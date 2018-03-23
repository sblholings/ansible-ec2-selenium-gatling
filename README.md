# ansible-ec2-selenium-gatling
ansible playbook to spin up new ec2 and install gatling, selenium and chrome web drivers 

Playbook has 3 roles and uses in memory and dynamic inventory to pick up details of newly created instances.

ASSUMPTIONS:
  ansible installed
  python2-pip installed
  boto installed
  aws cli
  ec2 instance has aws role attached (if running ansible from bastion host etc)
  ansible.cfg exists
  ssh-agent running
  pem file added to ssh

ec2:
  this role will launch the EC" instance in your configured region, please change variables based on your requirement in ec2/vars/main.yml

  key_name: create new one or use your own existing key (if using your own third party generated key, make sure to import .pub to aws).
  instance_type: choose your desired instance type.
  security_group: specify security group name or create a new one and allow ssh and other required ports.
  image: choose your ami based on your region.
  
Execution:

Before executing the playbook:

    1. place your pem file in the same location as the playbook.
    2. make sure your pem file has the appropriate read permissions
    3. define the path of your pem fiel in ansible config file (ansible.cfg)
        example: vi /etc/ansible/ansible.cfg
                # if set, always use this private key file for authentication, same as # if passing -- private-key to ansible or ansible-playbook private_key_file =
                /home/user/myfile.pem
    4. to avoid being prompted when task is being run for ssh, uncomment
       # uncomment this to disable SSH key host checking
         host_key_checking = False

  Then execute

    ansible-playbook -i ec2.py ec2-launch.yml

  *new ec2 instance will be launched, then Selenium, Gatling and Chrome Web Drivers be installed 
OTHER tasks can be created to configure and install packages on the new ec2 instance
