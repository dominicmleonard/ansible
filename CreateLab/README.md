Assuming you have cloned the repo to your Azure CloudShell, go to the folder in the CloudShell as in my example:

'dominic@Azure:~/ansibledev$ cd CreateLab/'
'dominic@Azure:~/ansibledev/CreateLab$ ls'

create-lab.yml  README.md  remove-resource-group.yml  vars.yml

Now you can run the Create-Lab.yml playbook to setup an Azure Resource Group with 2 VMs.

The Ubuntu VM will use the SSH keys you prepared already.

The playbook will prompt for a password for the Windows VM (user is set to 'azureadmin')

To run the playbook type:

dominic@Azure:~/ansibledev/CreateLab$ ansible-playbook create-lab.yml
