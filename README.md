# simple-ansible-to-start-Nginx
This is a simple ansible notebook for  playbook
## Task :
To install and start Nginx server 


# before starting 
Pre-requsite for ansible is password less
authentication
How to do
Step 1 ) generate key in main account
“ssh-keygen”
Step 2 ) go to id_rsa public and copy
Step 3) go to target account and in
authorized key paste the key 


# To run ansible 

ansible-playbook -vvv -i inventory
