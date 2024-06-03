# Why we need Ansible ??
  
When u go back to 2000 - 2010 there are system administrators doing configuration management.  

  __System administrators ( SA ):__   
- Theey are responsibel to key the physical inastances are in upto date. or alteast supported 
- system dependencies are in upto date  ( wget,ssh,pip, curl, yum etc )
- application dependencies are in upto date or supported version to application  
- maintenance of vms  

lets take some vms  
- ubuntu with centos  
- ubuntu with Debian  
- ubuntu with Alphine
- windows   
  
System Administrators manually maintain or update the dependencies by using shell scripting .  
when we want to update dependencies then we wants to write shell scriptting for centos, windows, debian seperately then it might difficult to handle those situation manually .  

To overcome this problems we have   
1) Puppet
2) Chef
3) Salt
4) Ansible  

SA ----> learn pullet and chefs language ----> write code  ----> install Agents in VMs ---->then puppet install the dependencies  

incase of __Ansible__   
SA ----> write code in YAML file  ----> Agent less ----> Ansible updates the VMs  

# Ansible Architecture

Ansible operates on a master-agent model, consisting of two primary types of nodes:

- **Control Node (Master)**: Also known as the Ansible controller node, this is the machine where you run Ansible commands. It communicates with the managed nodes to execute playbooks (YAML files ) and manage configurations.

- **Managed Node (Agent)**: These are the remote systems ( VMs ) that are being managed by Ansible. They receive instructions from the control node to apply changes, install packages, update configurations, and more.

## Relationship Between Control Node and Managed Nodes

The control node manages the execution of tasks on the managed nodes. Here's a simplified view of how they interact:

- The control node sends out tasks or playbooks to the managed nodes.
- Managed nodes execute the received tasks and report back to the control node.
- The control node collects the results and reports, allowing for automation and orchestration of IT tasks.

## Benifits of Ansible :  
1) __Agentless Architecture__ - Reduces overhead and simplifies management.  
2) __Idempotency__ - Ensures consistency across deployments.  
3) __Infinite Configuration Management__ - Offers powerful and flexible configuration management.  
4) __Multi-Node Deployment__ - Manages thousands of nodes efficiently.  
5) __Ad-hoc Command Support__ - Supports quick tasks and troubleshooting.  
6) __Integration Capabilities__ - Integrates seamlessly with other tools and services.
7) __Declarative Syntax__ - Improves readability and maintainability.  
8) __Security__ - Ensures encrypted communications and minimal permissions.  
   

## Ansible Usage Scenarios

- **Infrastructure Automation**: Config mgmt, app deploy, cloud provisioning
- **Network Automation**: Device config
- **Security Compliance**: Policy enforce
- **CI/CD**: Pipeline auto
- **IT Ops**: Routine tasks, troubleshooting
- **Cross-Platform**: Linux/Unix, Docker
- **Scalability**: Large deployments
- **Collaboration**: Team workflows

## What is Ansible ??  
Ansible is a simple powerful automation tool used for configuring systems, deploying software, and orchestrating more complex IT tasks.  

## Shell vs Python vs Ansible  
when we want to install java in VMs it is difficult for windows VM by using __Shell Scriptting__ instead we can use __python__ but we need to maintaine individual VMs that is againg difficult so go with __Ansible__ because of Agentless Architecture 