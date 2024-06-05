```
git clone https://github.com/atulkamble/ansible-ec2-webservers.git
cd ansible-ec2-webservers
```

# ansible-ec2-webservers

```
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

sudo httpd -version
sudo httpd -t
sudo httpd -V | grep SERVER_CONFIG_FILE
sudo systemctl status httpd.service
sudo systemctl stop httpd.service
sudo systemctl start httpd.service

sudo nginx -v
sudo nginx -t
sudo systemctl status nginx
sudo systemctl stop nginx
sudo systemctl start nginx

ansible-playbook --syntax-check playbooks/nginx.yml
ansible-playbook -vvvv ping.yml
```
