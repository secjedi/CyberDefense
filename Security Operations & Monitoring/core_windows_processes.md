We need to understand the normal behaviour of windows OS (create a baseline) so we can identify malicious processes running on endpoints. Anti-virus is the first solution for defensive approach. Then we have EDRs because anti virus cannot catch every malicious software
if one of the defense tools alerts us about a malicious process, we must investigate and decide a course of action. We must know the normal behaviour of the system that we are defending and we must infer if the binary is benign or evil. <br />

We can monitor process running on a system via `Task Manager`. In the Details tab, we can sort by `PID`s and add columns to the give us a better understanding of the process. Useful columns to add are `Image path name` and `Command line.`
![alt text](https://github.com/secjedi/CyberDefense/blob/main/Images/zerologon/7.png) <br /

