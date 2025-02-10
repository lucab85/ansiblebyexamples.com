---
title: "How to Install Ansible on Ubuntu 24.04 LTS Noble Numbat"
summary: "Learn how to install Ansible on Ubuntu 24.04 LTS (Noble Numbat) with a straightforward `sudo apt install ansible` command."
authors:
    - luca
date: 2024-04-22
---

## Introduction

In the rapidly evolving landscape of IT infrastructure management, Ansible emerges as a beacon of efficiency and simplicity. This open-source tool, championed by Red Hat, automates complex IT tasks and provides a user-friendly interface that simplifies the process of managing large-scale systems. This article delves into the practical application of Ansible in managing Ubuntu systems, using a real-world session log to illustrate its integration and efficacy.

The integration of Ansible into Ubuntu systems provides significant security benefits. By automating the patch management process, Ansible ensures that all systems are up-to-date with the latest security patches, reducing the risk of vulnerabilities. Additionally, Ansible's agentless architecture minimizes the system's attack surface, as it does not require additional software installed on the client machines.

<iframe width="560" height="315"
src="https://www.youtube.com/embed/1LhV87kjHlo"
frameborder="0" allowfullscreen>
</iframe>

## Instructions

Here is a step-by-step guide to securely connect to an Ubuntu 24.04 server and install Ansible for automation tasks:

### Step 1: Establishing SSH Connection

1.  Open Terminal: Start by opening your terminal on your local machine.
2.  Connect via SSH: Use the SSH command to initiate a secure connection:

```bash
ssh devops@ubuntu.example.com
```

1.  Replace `devops` with your actual username and `ubuntu.example.com` with your server's hostname or IP address.
2.  Verify Host Authenticity: Upon first connection, you'll be asked to verify the host's fingerprint:

The authenticity of host 'ubuntu.example.com (192.168.246.145)' can't be established.\
ED25519 key fingerprint is SHA256:WJG2h7cUirgFb3aXxeQkwvUJfE76ea21+U3mTD23tOQ.\
Are you sure you want to continue connecting (yes/no/[fingerprint])?

1.  Type `yes` to continue if you recognize the fingerprint.
2.  Enter Password: Input your user password when prompted to establish the connection.

### Step 2: Initial Server Setup and Updates

1.  Check for Updates: Once connected, check for available updates:

```bash
sudo apt update
```

1.  This command updates the list of packages and their versions on your server but doesn't install them.
2.  Upgrade Packages: Optionally, you can upgrade all your system software to the latest available versions:

```bash
sudo apt upgrade
```

1.  Confirm the prompt with `y` to proceed with the upgrades.

### Step 3: Installing Ansible

1.  Install Ansible: After updating your system, install Ansible using:

```bash
sudo apt install ansible
```

```bash
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  ansible-core python3-argcomplete python3-dnspython python3-jmespath python3-kerberos\
  python3-libcloud python3-lockfile python3-ntlm-auth python3-packaging python3-passlib\
  python3-requests-ntlm python3-resolvelib python3-selinux python3-simplejson\
  python3-winrm python3-xmltodict
Suggested packages:
  cowsay sshpass python3-trio python3-aioquic python3-h2 python3-httpx python3-httpcore\
  python-lockfile-doc
The following NEW packages will be installed:
  ansible ansible-core python3-argcomplete python3-dnspython python3-jmespath
  python3-kerberos python3-libcloud python3-lockfile python3-ntlm-auth
  python3-packaging python3-passlib python3-requests-ntlm python3-resolvelib
  python3-selinux python3-simplejson python3-winrm python3-xmltodict
0 upgraded, 17 newly installed, 0 to remove and 67 not upgraded.
Need to get 19.6 MB of archives.
After this operation, 316 MB of additional disk space will be used.
Do you want to continue? [Y/n] Y
```

1.  This command installs Ansible along with its dependencies. Confirm the installation by typing `y` when prompted.
2.  Verify Installation: Check the installed version of Ansible to ensure it is correctly installed:

```bash
ansible --version
```

```bash
ansible [core 2.16.3]
  config file = None
  configured module search path = ['/root/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python3/dist-packages/ansible
  ansible collection location = /root/.ansible/collections:/usr/share/ansible/collections
  executable location = /usr/bin/ansible
  python version = 3.12.3 (main, Apr 10 2024, 05:33:47) [GCC 13.2.0] (/usr/bin/python3)
  jinja version = 3.1.2
  libyaml = True
```

1.  This will display the version and configuration details of Ansible.

### Step 4: Configuring Ansible (Optional)

1.  You can generate the default configuration file using the command:

```bash
ansible-config init --disabled > ansible.cfg
```

1.  Configure Ansible: You can modify Ansible's configuration settings by editing its configuration file:

```bash
sudo nano /etc/ansible/ansible.cfg
```

1.  Make necessary changes such as default inventory file, privilege escalation settings, etc., according to your requirements.
2.  Create Inventory File: Ansible uses an inventory file to keep track of the servers it manages. Create a new inventory:

```bash
sudo nano /etc/ansible/hosts
```

1.  Add your servers under appropriate groups for better organization.

```bash
localhost ansible_connection=local
```


### Step 5: Testing Ansible Connection

1.  Test Connection: Run a simple Ansible command to check if Ansible can connect to the servers listed in your inventory file:

```bash
ansible all -m ping
```

1.  This command tests connectivity to all hosts in your inventory using the ping module. This is the expected output:

```bash
localhost | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
```

## Additional Tips

-   Secure SSH: Consider configuring SSH key-based authentication for a more secure and convenient server access method.
-   Regular Updates: Regularly update your server's packages and security patches using `apt update` and `apt upgrade`.
-   Ansible Playbooks: Start creating Ansible playbooks to automate more complex IT tasks across your servers.

By following these steps, you'll have a secure and functional setup for managing and automating tasks on your Ubuntu 24.04 server using Ansible. This setup provides a robust foundation for scaling your infrastructure management tasks efficiently.

## Conclusion

The use of Ansible in managing Ubuntu systems exemplifies the transformative impact of automation in IT operations. The session log provides a concrete example of how Ansible can be integrated into existing workflows to enhance efficiency, security, and manageability. As IT environments continue to grow in complexity, the role of automation tools like Ansible becomes increasingly critical. By embracing these tools, organizations can significantly reduce operational overheads and enhance their ability to respond swiftly to changing technological landscapes.

In summary, the practical application of Ansible in Ubuntu systems not only streamlines operations but also fortifies them against security threats, proving itself as an indispensable tool for modern IT infrastructure management.