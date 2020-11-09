1. Open Azure Cloud Shell (bash)
2. Create a key pair for ssh with command:
   
2. download key.pem file
3. when VM is provisioned use azure cloud shell to upload 'key.pem' file to cloud drive
4. create .ssh directory and move 'key.pem' file there:
$ mkdir .ssh
$ mv key.pem .ssh
5. now find your VM's IP Address by running:
dominic@Azure:~$ az vm show -g ansibledev -n anc01 -d --query publicIps
"51.137.130.107"
dominic@Azure:~$ ssh -i .ssh/anc01_key.pem azureuser@51.137.130.107
The authenticity of host '51.137.130.107 (51.137.130.107)' can't be established.
ECDSA key fingerprint is SHA256:jSykWmRMtV//zfP/clacFy+bDAvq0kf2YJ0n2e9LuI0.
Are you sure you want to continue connecting (yes/no)? yes

then you will be in the anc01 ubuntu machine:
azureuser@anc01:~$

6. sudo l
7. sudo apt update
8. sudo apt install ansible
9. sudo apt install python-pip
10. pip install "pywinrm>=0.2.2"
11. pip install "pypsexec"
 once complete run 'ansible --version' and you should see:

 azureuser@anc01:~$ ansible --version
/usr/lib/python2.7/dist-packages/ansible/parsing/vault/__init__.py:44: CryptographyDeprecationWarning: Python 2 is no longer supported by the Python core team. Support for it is now deprecated in cryptography, and will be removed in a future release.
  from cryptography.exceptions import InvalidSignature
ansible 2.9.15
  config file = /etc/ansible/ansible.cfg
  configured module search path = [u'/home/azureuser/.ansible/plugins/modules', u'/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python2.7/dist-packages/ansible
  executable location = /usr/bin/ansible
  python version = 2.7.17 (default, Sep 30 2020, 13:38:04) [GCC 7.5.0]

12. Now create a Windows Server VM in the same resource group as the anc01 server, take note of the username / password you set in creating it.
13. When deployment of Windows VM is complete we need to open up the SMB Firewall rule, so that later we can use Ansible to configure WinRM for us..
We can do this by invoking a PowerShell script inside the VM from the Azure cli.
in your CloudShell, exit out of the ubuntu server (if you're still ssh'd into it).
create a PowerShell script called openSMB.ps1 on your cloud drive with the following contents:
set-netfirewallrule -name 'FPS-SMB-In-TCP' -enabled true
now run that script inside your VM, like this:
az vm run-command invoke  --command-id RunPowerShellScript --name winserver01 -g ansibledev --scripts @openSMB.ps1

14. When complete, grab its private IP Address like this:
dominic@Azure:~$ az vm show -g ansibledev -n winserver01 -d --query privateIps
"10.0.0.5"

15. Now ssh back in to anc01
dominic@Azure:~$ ssh -i .ssh/anc01_key.pem azureuser@51.137.130.107

16. now make an ansibledev directory:
azureuser@anc01:~$ mkdir ansibledev
azureuser@anc01:~$ cd ansibledev/
azureuser@anc01:~/ansibledev$

17. copy ansible.cfg / hosts / vars.yml / set-winrm-options.yml from my git hub

18. 
    