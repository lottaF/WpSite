# WpSite - Worldpress Site
Provisions a worldpress site consisting of autoscaled apache webservers with access to an EFS and an RDS.

Initially use the default network.

Contains two CLoudformation stack files:
WPAnnVPC.yaml       - Siteetting up a new VPC with two public subnets in separate availability zones.
myWordPress.yaml    - Setting up the resources to accomplish the actual Wordpress solution consisting of:
                      - an EFS file system shared between the EC2 instances
                      - an RDS with a mariadb database, accessible from the two subnets
                      - a couple of Wordpress web servers (One in each AZ/subnet)
                      - a load balancer (ALB) receiveng the web requests
                      Wordpress is installed and configured by an EC2 instance.
Instructions:

    Open the file ’WPAnnVPC.yaml’, check (and possibly edit) the input-parameters declared in
    top of file. These parameter can be left with the default values.
    
        Environment:    Name of the VPC and used as prefix in network resources.
                        Default is ’MyCloud’.
        VpcCIDR:        IP range for the network in CIDR notation. 
                        If the pre-defined range is free and preferred, there is no need to 
                        update this nor the subnetwork IP ranges.
        PubSubn1CIDR:   IP range for one subnetwork. (Will be placed in AZ1)
        PubSubn2CIDR:   IP range for the other subnetwork. (Will be placed in AZ2)
 
    Build a stack based on this file.
    
    Then open the file ’myWordPress.yaml’, check and edit the input-parameters declared in top of file.
    From the utput of the "Ann-VPC stack", copy result into the parameters of 'VeraALB' as follows:
      

        MyVpc: 	    Copy Value of ’VPC’ in Output.
        MyPubSubn1:	Copy Value of ’ PubSubn1’ i Output.
        MyPubSubn2	Copy Value of ’ PubSubn2’ i Output.

    Set remaining parametrar as this:
    
    DevEnvCIDR:     State the IP range of the development environment that need ssh-access.
  
    NameSuffix:     State the name to mark the WP servers.

    KeyPairKey: 	State the name of the security key to use when generating the webservers.



