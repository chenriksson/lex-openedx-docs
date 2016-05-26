#SSH Tutorial

##Requirements
* [Git](http://www.git-scm.com/download/win)

##Security Notices

[CVE-2016-0777](https://www.qualys.com/2016/01/14/cve-2016-0777-cve-2016-0778/openssh-cve-2016-0777-cve-2016-0778.txt): For OpenSSH clients older than 7.1p2 (1/14/16), you should disable roaming to protect your private key.

  * Add "UseRoaming no" to your SSH configuration
  
    * Global configuration: /etc/ssh/ssh_config
    
      *Windows/Git Path: %ProgramFiles%\Git\etc\ssh\ssh_config*
    
    * User configuration: ~/.ssh/config
    
      *Windows/Git Path: %HOMEPATH%\\.ssh\ssh_config*
      
##Generating SSH Keys

See: [Generating RSA Keys](https://help.ubuntu.com/community/SSH/OpenSSH/Keys#Generating_RSA_Keys)

Run the following in Git Bash. By default, ssh-keygen uses KeyFile *'~/.ssh/id_rsa'* and prompts for PassPhrase.

`ssh-keygen -t rsa [-f KeyFile] [-N PassPhrase]`

##Copying SSH Public KeyFile

See: [Transfer Client Key to Host](https://help.ubuntu.com/community/SSH/OpenSSH/Keys#Transfer_Client_Key_to_Host)

Run the following in Git Bash. By default, ssh-copy-id uses PublicKeyFile *'~/.ssh/id_rsa.pub'*, Port 22, and current username.

`ssh-copy-id [-i PublicKeyFile] [-p Port] [user@]hostname`

##Connecting with SSH keys

Run the following in Git Bash. By default, ssh uses Port 22 and current username. If the PublicKeyFile is not provided, ssh will use the configured key file or password authentication.

`ssh [-i PublicKeyFile] [-p Port] [user@]hostname`

To configure SSH to use a specific PublicKeyFile every time, add an entry like the following to ~/.ssh/config:

`
HOST {hostname}
    User {user}
    IdentityFile /c/Users/{localUser}/.ssh/id_rsa
`

##Troubleshooting

* Error: Permission denied

  Enabled authentication methods appear after the message: "Permission denied (publickey, password)". If password is missing, it means password authentication has been disabled.

* Error: Host key verification failed

  When first connecting, you will see prompt 'Are you sure you want to continue connecting'. If you agree, a host entry will be added to file ~/.ssh/known_hosts.

  If the remote host changes (i.e., reimage), you will need to remove the old host entry from ~/.ssh/known_hosts.

  See: [More troubleshooting](https://help.ubuntu.com/community/SSH/OpenSSH/Keys#Troubleshooting)