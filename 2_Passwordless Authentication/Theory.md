# Passwordless Authentication:

![](https://res.cloudinary.com/practicaldev/image/fetch/s--N7bVEnyF--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/33ympesmiwld52do90ji.png) 

In General whenever we want to install something on VMs we write an YAML file or by using Adhoc commands. The  Control Node  transfers the commands to instances to perform the action but the instance need an authentication to perform that action.

This authentication is done in 2 ways:  
1) ssh with pem files  
2) password  
   
every time for every instance to provide a password is not a valid way of automation.
so that __passwordless authentication__ is the pre requisite which resolves the problem.  

In both the ways only for the 1st time connection we provide password or ssh key. And by using this passwordless mechanism, in future we are not going to provide any password or ssh key.


## Authentication using ssh with pem file  
  
    ssh-copy-id -f "-o IdentityFile <PATH TO PEM FILE>" ubuntu@<INSTANCE-PUBLIC-IP>  

when we connect to instance by using this command then next time there is no requirement to provide pem file .
  
    ssh ubuntu@<INSTANCE-PUBLIC-IP>  

## using Password  
Step 1: Connect to instance by using this command  
  
    ssh -i <path-to-pem-file> ubuntu@<instance-public-ip>
    sudo su -  

Step 2: go to the path  
  
    vim /etc/ssh/sshd_config.d/60-cloudimg-settings.conf  

Step 3: change the line  PA from no to yes then save the file
  
    PasswordAuthentication yes

Step 4: then restart the SSH process 
  
    systemctl restart ssh  

Step 5: create a password for ubuntu user  
  
    passwd ubuntu  

Step 6: logout then log backin  
  
    ssh-copy-id ubuntu@<public-ip-address>  
It asks password ,provide password  

Step 7: then try this command  
  
    ssh ubuntu@<INSTANCE-PUBLIC-IP>