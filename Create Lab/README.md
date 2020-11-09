1. Open Azure Cloud Shell (bash)

2. Create a key pair for ssh with command:
   ssh-keygen -m PEM -t rsa -b 4096

   accept the defaults, this will put a pub/privaye key pair in the default location on your clouddrive:
   $HOME/.ssh/id_rsa
   $HOME/.ssh/id_rsa.pub

3. Make a new local dir for github repo
   
   mkdir ansiblerepo

4. Clone my repo locally:

   