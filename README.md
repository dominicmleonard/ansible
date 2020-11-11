# README

* Login to Azure CloudShell (bash).

* Prepare SSH Key pair

    `ssh-keygen -m PEM -t rsa -b 4096`

    accept the defaults

* Clone my repo locally:

    `git clone https://github.com/dominicmleonard/ansible`

* When the repo is cloned go to the CreateLab folder and run:

    `ansible-playbook create-lab.yml`

* When that playbook has completed run:

    `ansible-playbook install-ansible.yml`

The first playbook creates 2 VMs (one Ubuntu and one Windows) in a resource group called 'devansible' in your Azure subscription.  It sets up the Windows VM's WinRM configuration so that Ansible can manage it.  It also dynamically creates 'inventory' and 'ansible.cfg' files that are used by the second playbook to install Ansible on to Ubuntu VM.

The second playbook uses the dynamically created files to install Ansible on the Ubuntu VM.

* You can set the VMs in the Resource Group to automatically shutdown (and thereby save money) by running this playbook in the CreateLab folder:

    `ansible-playbook set-scheduled-shutdown-for-vms.yml`

    If you accept the defaults it will setthe VMs in 'devansible' to shutdown at 17:30.  You could use this playbook to set shutdown schedules for VMs in any other Azure Resource Group.

* You can remove the resource group (and all resources created) by running this playbook in the CreateLab folder:

    `ansible-playbook remove-resource-group.yml`

    If you accept the default it will delete 'devansible' - you could use it to remove any Azure resource group by typing its name when prompted.
