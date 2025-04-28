```
git clone https://github.com/atulkamble/ansible-ec2-webservers.git
cd ansible-ec2-webservers
```
# tips
```
1. From AWS EC2 Console >> Create Keypair >> Replace keypair path
2. sign in as root >> su >> enter password
```
# ansible-ec2-webservers

```
// update host setting inventory/hosts
[webservers-apache]
13.200.222.115

[webservers-nginx]
13.235.78.187

sudo touch apache.yml
sudo nano apache.yml
sudo touch nginx.yml
sudo nano nginx.yml

ansible-playbook -i inventory/hosts playbooks/apache.yml
ansible-playbook -i inventory/hosts playbooks/nginx.yml
ansible-playbook -i inventory/hosts apache.yml
ansible-playbook -i inventory/hosts nginx.yml

// apache server
sudo httpd -version
sudo httpd -t
sudo httpd -V | grep SERVER_CONFIG_FILE
sudo systemctl status httpd.service
sudo systemctl stop httpd.service
sudo systemctl start httpd.service

// nginx server
sudo nginx -v
sudo nginx -t
sudo systemctl status nginx
sudo systemctl stop nginx
sudo systemctl start nginx

ansible-playbook --syntax-check playbooks/nginx.yml
ansible-playbook -vvvv ping.yml

ansible-playbook -i inventory/hosts playbooks/nginx.yml
ansible-playbook -i inventory/hosts playbooks/apache.yml
```
//setup//
ansible 
controle-node
1}sudo apt update
2}sudo apt-add-repository ppa:ansible/ansible
3}sudo apt update
4}sudo apt install ansible -y  
5}ssh-keygen 
6}  sudo cat /home/ubuntu/.ssh/id_ed25519.pub 
7}sudo vi /etc/ansible/hosts    
 8} [webservers]
web01 ansible_host=172.31.88.213 ansible_user=ubuntu
9} ansible webservers -m ping    
10} history

 manage-nod-01 
1}cd .ssh 
2} chmod 600 ~/.ssh/authorized_keys
3} sudo vi authorized_keys
4}chmod 700 ~/.ssh
5}chmod 600 ~/.ssh/authorized_keys
6} history
