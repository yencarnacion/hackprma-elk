REMEMBER to create env variables:

export DNSIMPLE_EMAIL
export DNSIMPLE_API_TOKEN
export AWS_ACCESS_KEY_ID
export AWS_SECRET_ACCESS_KEY


ansible -m ping  mqttserver
ansible -m debug -a "var=hostvars['inventory_hostname']" mqttserver
ansible all -m setup
ansible mqttserver --sudo -m raw -a "apt-get update; apt-get install -y python2.7 python-simplejson"


Steps:
#provision
ansible-playbook startmeup.yml 

ansible-playbook getstaticip.yml  

# verify
ansible mqttserver -m setup  

# destroy
ansible-playbook shutmedown.yml 
 
# provision xenial server with python 2.7
ansible-playbook step-02-install-python.yml 


# if machine already running, associate elastic ip with 
ansible localhost -m ec2_eip -a "device_id=i-7b50befd ip=23.20.127.95 in_vpc=yes region=us-east-1 "
