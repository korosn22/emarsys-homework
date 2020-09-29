# Kőrös Norbert's Emarsys homework solution

This solution was built on top of Ansible configuration management tool, which creates the necessary Google Cloud resources to host a very basic website based on LAMP stack on Centos 8.

1. Prerequisites for using this solution
    - Ansible version 2.8 (recommended 2.9)
    - Python version 3.7 with "requests" and "google-auth" libraries installed
      > pip3 install requests google-auth
    - GCP project named "emarsys-homework"
    - GCP service account JSON access file with sufficent privileges to administer GCP Compute Cloud resources at least in the project scope through API placed in reporitory root directory and named "emarsys-homework-acess.json"
    - Providing environmental variables:
      > export GCP_USERNAME=
      
      > export DB_USER_PASSWD=
    - The user who runs the ansible script has to have sudo access to the control machine in order for the local alma.com hosts file resolution to work (preferably nopasswd sudo access) 
    - Ubuntu 20.04 as a control machine is recommended (solution developed and tested in WSL Ubuntu 20.04)

2. Solution description
    - The script consists of two roles; the first one creates and configures GCP resources, the second prepares the OS to serve the required PHP script which makes the local database connection, and has access to a blank test database
    - The script deploys resources in europe-west region, and uses e2-standard-2 instance type
    - The main playbook aggregates the role execution and executes some misc. tasks on localhost
    - The task names are for documentation purposes as well, they describe what a task performs in great enough detail
    - The script restricts access to the resources to be reachable from a single public IP of the control machine on port 22 and 80
    - The provided PHP script was slightly modified with retained functionality to better fit the current PHP version
    - The solution does not prompt for variables to prevent manual action needed during script runtime, so it can be more easily integrated into a CI/CD pipeline with Env. variables
    - to run the script after configuration execute the following command:
      > ansible-playbook emarsys_homework.yml
    

The solution can be further expanded in several ways:
- OS and MySQL hardening
- TLS implementation
- Advanced error handling in Ansible playbooks and cleanup feature
- GCP access hardening with Ansible Vault

These might be implemented in the future in a more general approach to provide a general purpose simple webpage deploy kit on GCP.

Some notes about developing this solution:
- I had no prior experience on the GCP platform, so the solutions might have a couple of rough edges
