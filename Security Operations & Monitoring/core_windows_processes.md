We need to understand the normal behaviour of windows OS (create a baseline) so we can identify malicious processes running on endpoints. Anti-virus is the first solution for defensive approach. Then we have EDRs because anti virus cannot catch every malicious software
if one of the defense tools alerts us about a malicious process, we must investigate and decide a course of action. We must know the normal behaviour of the system that we are defending and we must infer if the binary is benign or evil. <br />

##### Task Manager
We can monitor process running on a system via `Task Manager`. In the Details tab, we can sort by `PID`s and add columns to the give us a better understanding of the process. Useful columns to add are `Image path name` and `Command line.`
![alt text](https://github.com/secjedi/CyberDefense/blob/main/Images/zerologon/7.png) <br />

These columns easily aleter us about outliers. For example, looking at the svchost.exe process with PID 876.<br />
![alt text](https://github.com/secjedi/CyberDefense/blob/main/Images/zerologon/8.png) <br />

So **Hint 1**: Check the command line and Image Path name and compare to normal behaviour. <br/>
If it is not what it appears to be at the Image path name and command line, we can perform a deeper analysis. <br />

The shortcoming for Task Manager is that it doesn't have the colum =n, parent process information, which is a powerful way to detect outliers. For example, if service.exe parent process is not service.exe, we perform a deeper analysis. <br />

![alt text](https://github.com/secjedi/CyberDefense/blob/main/Images/zerologon/9.png) <br />
**Hint 2**: Parewnt procees must align with child process. <br />


##### Process Hacker and Process Explorer
![alt text](https://github.com/secjedi/CyberDefense/blob/main/Images/zerologon/10.png) <br />
![alt text](https://github.com/secjedi/CyberDefense/blob/main/Images/zerologon/11.png) <br />

Asides from task manager, I should be familiar with processes on a Windows system: `tasklist`, `Get-Process` or `ps` (PowerShell), and `wmic`. <br />

Use Process Explorer to view properties of System
![alt text](https://github.com/secjedi/CyberDefense/blob/main/Images/zerologon/12.png) <br />
We can see that a lot of info is unvaialbe so if we check with process hacker, we get some more information. <br />
![alt text](https://github.com/secjedi/CyberDefense/blob/main/Images/zerologon/13.png) <br />




