
# Ansible Notes

Ansible is a powerful configuration management and automation tool that helps in managing infrastructure, deploying applications, and automating IT tasks. Below are some essential concepts and examples to get started with Ansible.

## Setting Up Passwordless SSH Connection

To enable passwordless connections between the Ansible controller and target nodes:

1. Run `ssh-keygen` on your Ansible control node to generate an SSH key pair.
2. Copy the public key to each target server with the following command:
3. Ensure that the public key is added to the authorized keys on the target servers.

## Inventory File

The inventory file in Ansible lists all the target nodes (IP addresses or hostnames) that Ansible will manage. Nodes can be grouped (e.g., web servers, database servers) to apply configurations selectively.

**Example Inventory File:**

```ini
[web]
1.1.1.1
2.2.2.2

[db]
3.3.3.3
4.4.4.4
```

In this example, `web` and `db` are groups, and Ansible can target them individually or all at once.

## Ad-hoc Commands

Ad-hoc commands are used for one-time tasks and do not require a playbook. They are helpful for quick, simple tasks.

**Example Ad-hoc Command:**

```bash
ansible -i inventory all -m shell -a "touch devopsclass"
```

This command touches a file named `devopsclass` on all target servers listed in the inventory.

### Common Ad-hoc Commands

- **Ping all hosts:**
  ```bash
  ansible -i inventory all -m ping
  ```

- **Check uptime:**
  ```bash
  ansible -i inventory all -m shell -a "uptime"
  ```

## Playbook

A playbook is a YAML file that defines a series of tasks to be executed on target nodes. Playbooks can automate complex workflows by chaining multiple commands together.

### Example Playbook

Here is an example of a simple playbook to install and start the `nginx` web server:

**first_playbook.yml:**

```yaml
---
- name: Install and start NGINX
  hosts: web
  become: yes
  tasks:
    - name: Install NGINX
      apt:
        name: nginx
        state: present

    - name: Start NGINX service
      service:
        name: nginx
        state: started
```

To run the playbook, use the following command:

```bash
ansible-playbook -i inventory first_playbook.yml
```

### Notes

- `hosts: web` specifies that this playbook should only run on nodes in the `web` group.
- `become: yes` is used to run tasks with elevated (root) privileges.
- Tasks can include modules such as `apt` for package installation and `service` to manage services.

## Grouping Servers in Inventory

To target different types of servers, such as `web` and `db`, group them in the inventory file and use group names in playbooks and ad-hoc commands.

**Example:**

```ini
[web]
1.1.1.1
2.2.2.2

[db]
3.3.3.3
4.4.4.4
```

## Additional Resources

- For more commands and detailed usage, refer to the [Ansible Documentation](https://docs.ansible.com/).
- Explore module documentation within Ansible by running:
  ```bash
  ansible-doc <module_name>
  ```
