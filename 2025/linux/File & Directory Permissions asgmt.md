File & Directory Permissions


Task:

Create /devops_workspace and a file project_notes.txt.

## Commands Executed

1. Create a directory named `devops_workspace`:
   ```bash
   sudo mkdir devops_workspace
   ls -ld
   # output
   irwxr-x--- 5 bhoomika bhoomika 4096 Feb 10 18:16
   ls
   devops_workspace
   #create file
   sudo touch /devops_workspace/project_notes.txt
   sudo chmod 640 /devops_workspace/project_notes.txt
   #check the premissions
   ls -l /devops_workspace/project_notes.txt
   #output
   -rw-r----- 1 root root 0 Feb 10 18:17 /devops_workspace/project_notes.txt
