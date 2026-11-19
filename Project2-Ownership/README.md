\# Project 2: Windows File Ownership and Access Troubleshooting



\## 1. Project Overview



This project demonstrates Windows file ownership administration and NTFS permission troubleshooting using Command Prompt and PowerShell.



The objective was to identify a file's owner, change ownership to a test account, verify the change and investigate how inherited permissions affect user access.



\## 2. Lab Environment



\- Operating System: Windows 10/11

\- Tools: Command Prompt and PowerShell

\- Utilities: `icacls`, `Get-Acl`, `dir`, `whoami`, `runas`

\- Test account: `LabAlice`

\- Isolated testing directory: `C:\\LabTesting\\Ownership`



\## 3. Task 1: Identify the Original File Owner



Created a demonstration file named `ownership-demo.txt`.



```cmd

echo This file is for testing Windows file ownership. > ownership-demo.txt

```



Used the following commands to identify its owner:



```cmd

dir /q ownership-demo.txt

```



```powershell

(Get-Acl '.\\ownership-demo.txt').Owner

```



The original owner was identified as the current Windows user account.



\## 4. Task 2: Change File Ownership



Opened Command Prompt with Administrator privileges and executed:



```cmd

icacls ownership-demo.txt /setowner "%COMPUTERNAME%\\LabAlice"

```



The command successfully changed the file owner to LabAlice.



\### Verification



Verified the ownership change using:



```cmd

dir /q ownership-demo.txt

```



And:



```powershell

(Get-Acl '.\\ownership-demo.txt').Owner

```



Both methods confirmed LabAlice as the new owner.



\## 5. Challenges Encountered and Troubleshooting



\### Challenge 1: Access restrictions in the original Documents location



During testing, LabAlice encountered access restrictions when attempting to access files in the original Documents location.



\*\*Investigation:\*\*



The issue involved permissions on the parent directory, not simply the permissions on the individual file.



\*\*Action taken:\*\*



Created an isolated testing directory outside the repository:



`C:\\LabTesting\\Ownership`



This allowed testing without unnecessarily changing permissions on the personal Documents folder or Windows system directories.



\### Challenge 2: LabAlice could modify a file despite having RX on the folder



\*\*Problem:\*\*



LabAlice was explicitly granted Read and Execute (RX) on the isolated testing folder. However, she was also able to append content to the test file.



This was unexpected because the intention was to test limited access.



\*\*Investigation:\*\*



Inspected the folder and file ACLs using:



```cmd

icacls C:\\LabTesting\\Ownership

```



```cmd

icacls test-file.txt

```



The investigation revealed an inherited Modify (M) permission assigned to:



`NT AUTHORITY\\Authenticated Users`



LabAlice is an authenticated user, so this inherited permission also applied to her.



\*\*Verification:\*\*



Opened a separate Command Prompt as LabAlice:



```cmd

runas /user:%COMPUTERNAME%\\LabAlice cmd

```



Confirmed the account:



```cmd

whoami

```



Tested reading the file:



```cmd

type C:\\LabTesting\\Ownership\\test-file.txt

```



Tested appending content:



```cmd

echo Testing file modification as LabAlice. >> C:\\LabTesting\\Ownership\\test-file.txt

```



The new content appeared when the file was displayed again.



\*\*Finding:\*\*



The inherited Modify permission explained why LabAlice could modify the file despite having only an explicit RX entry on the folder.



The permission issue was identified but not yet corrected in this exercise.



\## 6. Key Technical Concepts Learned



\- File ownership and file permissions are separate concepts.

\- Changing ownership does not automatically change the file's ACL.

\- ACLs contain Access Control Entries (ACEs).

\- Permissions can be inherited from parent folders.

\- Users can receive permissions through individual accounts and group memberships.

\- Folder permissions and file permissions serve different purposes.

\- Effective access depends on all applicable permissions.



\## 7. Project Outcome



Successfully changed and verified Windows file ownership.



Investigated an unexpected file modification scenario, identified inherited Modify permissions as the cause and verified the behaviour using a separate test account.



\## 8. Skills Demonstrated



\- Windows file ownership administration

\- NTFS permissions and ACL inspection

\- Command Prompt and PowerShell

\- Local user account testing

\- Permission inheritance investigation

\- Access troubleshooting

\- Technical documentation

