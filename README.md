# Nextcloud_Ansible
Ansible Script for deploy nextcloud on Ubuntu 20.04

The runbook install nextcloud with the following addons:
- OnlyOffice office container
- apc cache
- notify_push
- ldap Connection
- mail service
- twofactor_totp
- drawio
- recognition
- external files include smb/cifs

# Run the playbook

## Update inventory
Set the hostname and IP Address to the `inventory.yaml` file.

## Update Vars
Before using the ansible-playbook you need to decalre the vars in the `vars.yaml` file and generate the passwords.

### Generate Passwords
> **_NOTE:_**  The `.vaultpw` file is ignored by `.gitignore`

1. Set a new vault password and save it to a new `.vaultpw` file. 
2. Encrypt the password and overwrite the encrypted string in the `passwords.yaml` file:
```bash
ansible-vault encrypt_string --vault-password-file .vaultpw --name 'db_pw' 'PasswortInKlartext' --encrypt-vault-id default
```

## Run Ansible
```bash
# With ssh and ssh-key
ansible-playbook -i inventory.yaml -u <user> -D main.yaml -c ssh

#With ssh, username and password
ansible-playbook -i inventory.yaml -u <user> -D main.yaml --ask-pass --ask-become-pass
```

## Troubleshooting

#### Install php-pear package
If you receive an error and you have to update the channel, please run the command given on the exception and run this step manual:
```bash
sudo pecl install smbclient
```

#### Configure facerecognition
If you have an error you have to define the values in the GUI. Go to Nextcloud Homepage > Settings > Face Recognition and set the values.
