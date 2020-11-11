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
