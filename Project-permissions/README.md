\# Project 1: Windows File Permissions



\## Objective

Learn how Windows NTFS file permissions control access to files.



\## Tools

\- Windows Command Prompt (CMD)

\- `icacls.exe`

\- `type`



\## Practical Work

\- Inspected file permissions using `icacls.exe`.

\- Identified Read (R), Read \& Execute (RX), and Full Control (F).

\- Identified inherited permissions using the (I) marker.

\- Displayed the file contents using `type`.

- Created a dedicated local test account named `LabAlice` using `net user`.
- Granted `LabAlice` Read permission on `permissions-demo.txt` using `icacls.exe`.
- Re-inspected the file's ACL to verify the permission entry.
- Confirmed that Read permission does not grant permission to modify file contents.



\## Key Concepts

\- ACL: Access Control List — the list of permission entries.

\- ACE: Access Control Entry — one individual permission entry.

\- NTFS: New Technology File System.

\- Explicit permissions are configured directly on a file or folder.

\- Inherited permissions come from a parent folder.

\- Access can be granted directly to a user or through group membership.



\## Safety Notes

Inspected permissions in a dedicated lab directory. No system-file permissions were changed.

