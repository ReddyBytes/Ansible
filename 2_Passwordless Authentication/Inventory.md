# Ansible Inventory

Imagine you're the manager of a restaurant kitchen.  
some chefs cooking meals, others cleaning dishes, and still others preparing ingredients.  
 To keep track of who does what, you might use a schedule or a board where you list everyone's tasks.  
 
 __Ansible Inventory acts like that schedule or board. It keeps track of all the computers (servers) you manage, organizing them into groups based on their roles or functions,__ just like how you'd organize your kitchen staff.  

## Types
__1) Static inventory :__   

A manually updated file listing servers and groups, ideal for small, stable environments.  
 It's straightforward but requires you to update it anytime there's a change in your servers.  

 These files are in 2 types  
1) inventory.ini  ---- recomended approach  
   
   we can put this  inventory.ini file in the below path so that there is no need to pass everytime when ansible is running
  
    /etc/ansible/inventory.ini  --> not recomended way
  
        # servers.ini
        [web_servers]
        server1.com IP=192.168.1.101
        #server2.com IP=192.168.1.102  
        ubuntu@192.168.1.102

        [database_servers]
        db1.com IP=192.168.1.103
        db2.com IP=192.168.1.104

usage:  
  
    ansible -i servers.ini -m ping all
    ansible -i servers.ini -m ping ubuntu@192.168.1.102  
    ansible -i servers.ini -m shell  web_servers
    
2. YAML file  ( playbooks files )
  
    
        # servers.yaml  
        all:  
            vars:
                ansible_user: admin
                ansible_ssh_private_key_file: /path/to/key
            children:
                web_servers:
                hosts:
                    server1.com:
                    ansible_host: 192.168.1.101
                    server2.com:
                    ansible_host: 192.168.1.102
                database_servers:
                hosts:
                    db1.com:
                    ansible_host: 192.168.1.103
                    db2.com:
                    ansible_host: 192.168.1.104

        
  
    
__2) Dynamic inventory :__ 

Automatically generates server lists from various sources like AWS, GCP, cloud sources perfect for large, dynamic environments.

Here is an example of a dynamic inventory script for AWS EC2:
  
    #!/usr/bin/env python

    import json
    import boto3

    def get_aws_ec2_inventory():
        ec2 = boto3.client('ec2')
        instances = ec2.describe_instances()
        inventory = {
            'all': {
                'hosts': [],
                'vars': {
                    'ansible_user': 'ec2-user',
                    'ansible_ssh_private_key_file': '/path/to/key'
                }
            },
            '_meta': {
                'hostvars': {}
            }
        }

        for reservation in instances['Reservations']:
            for instance in reservation['Instances']:
                if instance['State']['Name'] == 'running':
                    public_ip = instance['PublicIpAddress']
                    inventory['all']['hosts'].append(public_ip)
                    inventory['_meta']['hostvars'][public_ip] = {
                        'ansible_host': public_ip
                    }

        print(json.dumps(inventory, indent=2))

    if __name__ == '__main__':
        get_aws_ec2_inventory()

usage:  
  
    ansible-playbook -i inventory <Adhoc command or Playbook.yml>  

for more ad hoc commands [click here](https://docs.ansible.com/ansible/latest/command_guide/intro_adhoc.html#patterns-and-ad-hoc-commands)