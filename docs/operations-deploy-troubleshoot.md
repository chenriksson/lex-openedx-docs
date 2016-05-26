#Deploying Open edX on Azure: Troubleshooting

####Ansible hangs during installation

Intermittent issue seen on Cypress installations. Not sure if it reproduces with Dogwood.

Resolution: Kill all ansible processes and re-run the playbook.

  1. Tail the installation log to ensure that ansible really is hung. Has it been on the same task for >30-60 minutes?
  
  2. Search for and kill any ansible process groups. Multiple PGIDs means there are multiple parents (possibly multiple playbooks running).
  
  ```
  $ sudo ps x -o "%p %r %y %x %c" |grep ansible
  PID  PGID TTY          TIME COMMAND
  10978 10967 pts/5    00:00:39 ansible-playboo
  
  $ sudo kill -TERM -10967
  ```
  
  3. Search for and kill any remaining ansible processes, in case these weren't killed with the process group. If you are installing on multiple VMs (scalable), do this on each.
  
  ```
  $ ps aux | grep '[a]nsible'
    USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
    ...
    
  $ kill -9 {PID}
  ```
  
  4. Re-run the ansible playbook, preferrably in the background with stdout/stderr redirected in case your session is disconnected. Playbook command is available from the install-openedx.sh script in the ARM template repository.
