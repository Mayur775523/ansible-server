# ansible
ansible
📌 1. What is Ansible?

Ansible is provisioning and configuration management tool

- Open-source automation tool for :

Configuration management
Application deployment
Provisioning (e.g., cloud infrastructure)
- Uses SSH for communication (agentless).
- Written in Python, config in YAML (playbooks).
- Works on port 22
- Works on push based mechanism

✅ What is a Playbook in Ansible?
An Ansible playbook is a YAML file that defines a series of tasks to be executed on one or more remote hosts. It is the main way to automate configuration, deployment, and orchestration using Ansible.

📂 2. Directory Structure

project/
├── inventory.ini
├── playbook.yml
├── roles/
│   └── web/
│       ├── tasks/
│       │   └── main.yml
│       └── templates/
inventory files / hosts - Stores the vm's information
ansible.cfg - configuration file

📄 3. Inventory File (hosts)

The inventory file is a core component of Ansible. It tells Ansible which hosts to manage, and optionally, how to connect to them.

🗂️ What is an Inventory File?

A text file that lists the managed nodes (hosts).
You can group hosts and set variables like SSH user, port, and key.
Used in ad-hoc commands, playbooks, and roles.
Ansible Installation on ubuntu :

$ sudo apt update
$ sudo apt install software-properties-common
$ sudo add-apt-repository --yes --update ppa:ansible/ansible
$ sudo apt install ansible
command for take access of host machine :

ansible -i hosts all -u ubuntu --private-key=./new-key.pem -m shell -a hostname
command after adding username and private key in ansible.cfg file :

ansible -i hosts all  -m shell -a hostname
ansible -i hosts all  -m shell -a 'echo "Hello World"'
To run .yaml file

ansible-playbook first.yaml
Variables - name of memory location to store the data

Types of variable -

local varible - Defined within a play, task, or block using vars, valid only in that paricular block only
global variable - applies across all plays and hosts.
separate file variable - write in separate .txt file and called it when need
CLI variable ansible - passed in cli
playbook playbook.yml -e "variable_name=value"
register variable - captures the output of a task using the register keyword for use in later tasks.
prompt variable - ask user for input variable
host variable - defined per host in the inventory (static or dynamic), applying only to that specific host.
Ansible Variable Precedence (High to Low) -

CLI Variable - Defined using -e; highest precedence, overrides all others.
Prompt Variable - User input at runtime via vars_prompt; high precedence.
Local Variable - Defined with vars inside a play, block, or task.
Register Variable - Captures output of a task using register; available after task runs.
Separate File Variable - Variables from external files via vars_files or include_vars.
Host Variable - Defined per host in inventory; overrides group/global variables.
Global Variable - Set in ansible.cfg, environment vars, or inventory defaults; lowest.
Ansible Modules -

An Ansible module is a reusable, standalone script that performs a specific task on a target system — like installing packages, managing files, users, services, etc.

📘 Key Characteristics:

Modules are the building blocks of tasks in a playbook.
Each task in a playbook uses one module to do something.
Modules are idempotent — they make changes only if needed.
Ansible has hundreds of built-in modules and supports custom modules.
🧱 Example of Using a Module

- name: Install Apache using the yum module
 yum:
   name: httpd
   state: present
In this example:

yum is the module.
It ensures the package httpd is installed (state: present).
🔥 Commonly Used Modules

yum / apt - Install or remove packages
conditions: when - when perform
privilege (root user) - perform through root user
package - download particular package when we don't know package name
service / systemd - start, enable, stop, restart service
copy - copy files to remote host
file - manage file
line in file - add / remove particular line
block in file - add / remove particular block
tags -
