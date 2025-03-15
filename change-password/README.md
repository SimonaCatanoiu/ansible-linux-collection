# Change-linux-password

## Overview
`Change-linux-password` is an Ansible playbook designed to update root and admin passwords on Linux machines. Currently, the playbook has been tested exclusively on Ubuntu 22.

## 📜 Logging
After execution, a log file named `ansible_ping.log` will be generated in the `/playbooks` directory. This log file contains connection statuses for each host:

- ✅ `<hostname> <ip> - CONNECTED` → Successfully connected, password changed.
- ❌ `<hostname> <ip> - NO ROUTE TO HOST` → Host unreachable.
- 🔑 `<hostname> <ip> - INVALID ADMIN PASSWORD` → Incorrect admin password provided.
- 🔐 `<hostname> <ip> - INCORRECT ROOT PASSWORD` → Admin password correct, but root password incorrect.
- ⚠️ `<hostname> <ip> - UNREACHABLE (OTHER ERROR)` → Other types of connectivity errors.

## 🔒 Password Management
Old and new passwords are stored in `/global_vars/secrets.yaml` and encrypted using `ansible-vault` for security.

## 🚀 Usage

1. **Decrypt** the `/global_vars/secrets.yaml` file and update it with the old and new credentials.
2. **Re-encrypt** the `/global_vars/secrets.yaml` file.
3. **Specify** the target host IPs in `/inventory/hosts.ini`.
4. **Run** the playbook using the following command:
   ```sh
   ansible-playbook -i inventory/hosts.ini playbooks/main.yaml --ask-vault-pass
   ```

## ✅ Requirements
- Ansible installed on the control machine.
- Sudo or root access to target machines.
- Properly configured SSH access to target hosts.

## ⚠️ Notes
- Ensure that Ansible Vault is used to encrypt sensitive information.
- The playbook should be tested on non-production systems before deploying in a live environment.

