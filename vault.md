You can encrypt any structured data file used in Ansible, including:

ansible_facts

A variable file in host_vars

group_vars directories

Variable files loaded by 
include_vars keywords within a playbook

Variable files passed on the command line using the -e option followed by the name of the variable file (for example, -e @var_file.yml)
------------------------------------------------------------------
Creating Encrypted File
To create an encrypted file, use the ansible-vault create command and pass the filename.

$ ansible-vault create filename.yaml
You’ll be prompted to create a password and then confirm it by re-typing it. 

ansible vault create - Ansible Vault - Edureka

Once your password is confirmed, a new file will be created and will open an editing window. 
By default, the editor for Ansible Vault is vi. You can add data, save and exit. 

secrets txt - Ansible Vault - Edureka
And your file is encrypted.

edit output - Ansible Vault - Edureka
Editing Encrypted Files
If you want to edit an encrypted file, you can edit it using ansible-vault edit command.

$ ansible-vault edit secrets.txt
Where secrets.txt is an already created, encrypted file.

You’ll be prompted to insert the vault password. The file(decrypted version) will open in a vi editor and then you can make the required changes. 

vault edit - Ansible Vault - Edureka

If you check the output, you’ll see your text will be encrypted automatically when you save and close.

edit output - Ansible Vault - Edureka

Viewing Encrypted File
If you wish to just view an encrypted file, you can use the ansible-vault view command.

$ ansible-vault view filename.yml
Again you’ll be prompted for a password.

vault view - Ansible Vault - Edureka

and you’ll see similar output.

view output - Ansible Vault - Edureka
Rekeying Vault Password
Of course, there are times where you’ll want to change the vault password. You can use the ansible-vault rekey command.

$ ansible-vault rekey secrets.txt
You’ll be prompted with the vault’s current password and then the new password and finally done by confirming the new password.

rekey out - Ansible Vault - Edureka
Encrypting Unencrypted Files
Suppose you have a file which you wish to encrypt, you can use the ansible-vault encrypt command.

$ ansible-vault encrypt filename.txt
You’ll be prompted to insert and confirm password and your file is encrypted.

vault encrypt - Ansible Vault - Edureka
Now that you look at file contents, its all encrypted.

encrypt output - Ansible Vault - Edureka
Decrypting Encrypted Files
If you want to decrypt an encrypted file, you can use ansible-vault decrypt command.

$ ansible-vault decrypt filename.txt
As usual, it’ll prompt you to insert and confirm the vault password.

vault decrypt - Ansible vault - Edureka
Encrypting specific variables
Best practice while using Ansible Vault is to encrypt only the sensitive data. In the example explained above,
the development team does not want to share their password with the production and the staging team but 
they might need access to certain data to carry out their own task. In such cases you should only
be encrypting the data you do not want to share with others, leaving the rest as it is. 

Ansible Vault allows you to encrypt only specific variables. You can use the ansible-vault
encrypt_string command for this.

$ ansible-vault encrypt_string
You’ll be prompted to insert and then confirm the vault password. 
You can then start inserting the string value that you wish to encrypt. 
Press ctrl-d to end input. Now you can assign this encrypted value to a string in the playbook.

vault encrypt string - Ansible Vault - Edureka

You can also achieve the same thing in a single line. 

$ ansible-vault encrypt_string 'string' --name 'variable_name'
vault encrypt string - Ansible Vault - Edureka

Decrypting Encrypted Files During Runtime
If you wish to decrypt a file during runtime, you could use –ask-vault-pass flag.

$ ansible-playbook launch.yml --ask-vault-pass
This will decrypt all the encrypted files that are used for this launch.yml playbook to execute. 
Also, this is only possible if all the files are encrypted with the same password.

ask vault pass - Ansible Vault - Edureka

Password prompts can get annoying. The purpose of automation becomes pointless. How do we make this better?
Ansible has a feature called “password file” which references to a file containing the password. 
You can then just pass this password file during runtime to automate it.

$ ansible-playbook launch.yml --vault-password-file ~/ .vault_pass.txt
vault pass file - Ansible Vault - Edureka

Having a separate script that specifies the passwords is also possible. You need to make sure the script file is 
executable and the password is printed to standard output for it to work without annoying errors.

$ ansible-playbook launch.yml --vault-password-file ~/ .vault_pass.py
Using Vault Id
Vault Id is a way of providing an identifier to a particular vault password. Vault ID helps in encrypting different
files with different passwords to be referenced inside a playbook. This feature of Ansible came out with the release
of Ansible 2.4. Prior to this release, only one vault password could be used in each ansible playbook execution.

So now if you wish to execute an Ansible playbook which uses multiple files encrypted with different passwords, 
you can use Vault Id.

$ ansible-playbook --vault-id vault-pass1 --vault-id vault-pass2 filename.yml
With this, we come to the end of this Ansible Vault blog. It is amazing to catch up with technology and
make the fullest of them but not by compromising on security. This is one of the best ways to have Infrastructure as code(IaC). 
