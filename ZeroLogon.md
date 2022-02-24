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


