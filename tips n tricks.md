# Some Useful Tips

* Generate SSH Keys
  
  `ssh-keygen -m PEM -t rsa -b 4096`

* how to find public ip of a vm from az cli:

   `az vm show -g devansible -n ubuntu01 -d --query publicIps`

* how to find private ip of a vm from az cli

   `az vm show -g devansible -n ubuntu01 -d --query privateIps`

* how to quickly shutdown and deallocate all VMs in a resource group (so they no longer cost you money)

   `az vm deallocate --ids $(az vm list -g devansible --query "[].id" -o tsv)`
