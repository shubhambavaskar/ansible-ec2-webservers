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

 **Ansible Setup** 
---

#  Ansible Setup Process:

# 1. Install Ansible on the Control Node:

```bash
sudo apt update
sudo apt-add-repository ppa:ansible/ansible
sudo apt update
sudo apt install ansible -y
```
- ➡ This installs Ansible on your control node (example: an Ubuntu EC2 instance).

---

###  2. Create and Copy SSH Key:

```
ssh-keygen
```
- ➡ This command generates an SSH key pair (private and public keys).
- Default files: `/home/ubuntu/.ssh/id_rsa` (private) and `/home/ubuntu/.ssh/id_rsa.pub` (public).

```bash
cat ~/.ssh/id_rsa.pub
```
- ➡ View and copy your public key.

---

###  3. Setup on the Managed Node:

**On the managed node:**

```bash
cd ~/.ssh
sudo vi authorized_keys
```
- ➡ Paste the control node's public key inside the `authorized_keys` file.

**Fix file permissions:**

```
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```
- ➡ These permissions are very important for secure SSH communication.

---

###  4. Edit the Ansible Inventory File:

```
sudo vi /etc/ansible/hosts
```
**Add the following:**
```ini
[webservers]
web01 ansible_host=172.31.88.213 ansible_user=ubuntu
```
- ➡ `web01` is an alias (name you choose).
- ➡ `ansible_host` is the managed node's IP address.
- ➡ `ansible_user` is the SSH username (usually `ubuntu` on AWS).

---

### 📡 5. Test the Connection:

```
ansible webservers -m ping
```
- ➡ You should get "pong" response if everything is setup correctly.

---

# ✨ Important Points to Remember:

| Step | Why It's Important |
|:---|:---|
| `ssh-keygen` | Creates a key for passwordless SSH from control node to managed node. |
| `/etc/ansible/hosts` | Inventory file where you define servers (managed nodes). |
| `ansible -m ping` | To test if Ansible can reach the servers. |
| `chmod 700/600` | To secure SSH folder and files. |
| `ansible_user` | Defines the username Ansible should use to SSH into the managed node. |

---

# If You Have Multiple Servers:

Example inside `/etc/ansible/hosts`:

```ini
[webservers]
web01 ansible_host=172.31.88.213 ansible_user=ubuntu
web02 ansible_host=172.31.91.100 ansible_user=ubuntu
web03 ansible_host=172.31.92.150 ansible_user=ubuntu
```
- ➡ You can manage multiple servers easily by grouping them!

---------------------------------------------------------------------------------------------------------------------------------------------------------------
install_nginx.yml:

---
- name: Install and start nginx on webservers
  hosts: webservers
  become: true

  tasks:
    - name: Install nginx
      apt:
        name: nginx
        state: present
        update_cache: yes

    - name: Start nginx service
      service:
        name: nginx
        state: started
