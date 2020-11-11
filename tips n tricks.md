# Some Useful Tips

* Generate SSH Keys
  
  `ssh-keygen -m PEM -t rsa -b 4096`

* How to quickly shutdown and deallocate all VMs in a resource group (so they no longer cost you money - the VMs can be restarted at anytime.)

   `az vm deallocate --ids $(az vm list -g devansible --query "[].id" -o tsv)`

* You can set the VMs in the Resource Group to automatically shutdown (and thereby save money) by running this playbook in the CreateLab folder:

    `ansible-playbook set-scheduled-shutdown-for-vms.yml`

    If you accept the defaults it will setthe VMs in 'devansible' to shutdown at 17:30.  You could use this playbook to set shutdown schedules for VMs in any other Azure Resource Group.

* You can remove the resource group (and all resources created) by running this playbook in the CreateLab folder:

    `ansible-playbook remove-resource-group.yml`

    If you accept the default it will delete 'devansible' - you could use it to remove any Azure resource group by typing its name when prompted.

* how to find public ip of a vm from az cli:

   `az vm show -g devansible -n ubuntu01 -d --query publicIps`

* how to find private ip of a vm from az cli

   `az vm show -g devansible -n ubuntu01 -d --query privateIps`
