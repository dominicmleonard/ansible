# install ansible on ubuntu VM and then setup winrm on windows VM

1. Find your VM's IP Address by running this from the cloudshell (in my example vm name is ubuntu01, resourcegroup is devansible)

    `az vm show -g devansible -n ubuntu01 -d --query publicIps`

    `"52.138.196.98"`

    now ssh to the ip with the 

    `dominic@Azure:~$ ssh -i .ssh/id_rsa azureuser@52.138.196.98`

    then you will be in the ubuntu01 ubuntu machine:

    `azureuser@ubuntu01:~$`

2. `sudo apt-add-repository ppa:ansible/ansible`
3. `sudo apt update`
4. `sudo apt install ansible`
5. `sudo apt install python-pip`
6. `pip install "pywinrm>=0.2.2"`
7. `pip install "pypsexec"`

   once complete run `ansible --version` and you should see that it is installed.
   now exit out from the ubuntu ssh session.

8. By defult the Windows VM will have a Firewall rule that disables SMB to the server, we need to change the default so that later we can use Ansible to configure WinRM for us..
We can do this by invoking a PowerShell script inside the VM from the Azure cli.
in your CloudShell, exit out of the ubuntu server (if you're still ssh'd into it).
create a PowerShell script called openSMB.ps1 on your cloud drive with the following contents:

    `set-netfirewallrule -name 'FPS-SMB-In-TCP' -enabled true`

    now run that script inside your VM, like this:

    `az vm run-command invoke  --command-id RunPowerShellScript --name winserver01 -g devansible --scripts @openSMB.ps1`

9. When complete, grab its private IP Address like this:

    `dominic@Azure:~$ az vm show -g devansible -n winserver01 -d --query privateIps`

   `"10.0.0.5"`

10. Now ssh back in to ubuntu01
  `dominic@Azure:~$ ssh -i .ssh/id_rsa azureuser@52.138.196.98`

11. now make an devansible directory:
  `azureuser@ubuntu0:~$ mkdir devansible`
  `azureuser@ubuntu0:~$ cd devansible/`
  `azureuser@ubuntu0:~/devansible$`

12. now copy these files from my https://github.com/dominicmleonard/ansible/tree/master/SetupLab folder:

    `hosts`

    `set-winrm-options.yml`

13. run:

    `ansible-playbook set-winrm-options.yml`

    this will ask for the privateip address of the windows vm and its admin user / password

14. edit 'hosts' to have your windows VM's private IP and admin password

15. you can now run:

    `ansible Windows_Servers -i hosts -m win_ping`

    You should see a ping / pong