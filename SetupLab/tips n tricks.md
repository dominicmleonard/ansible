1. how to find public ip of a vm from az cli:

   az vm show -g devansible -n ubuntu01 -d --query publicIps

2. how to find private ip of a vm from az cli

   az vm show -g devansible -n ubuntu01 -d --query privateIps

3. how to quickly shutdown and deallocate all VMs in a resource group (so they no longer cost you money)

   az vm deallocate --ids $(az vm list -g devansible --query "[].id" -o tsv)