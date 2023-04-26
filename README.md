# Entrypoint

Set ansible-run as executable and run.
```bash
chmod +x ansible-run
./ansible-run
```
This will install Ansible.

Try to run local.yml
```bash
ansible-playbook local.yml --ask-vault-pass
```

This will put a decrypted copy of the private and public key in your local .ssh folder.
It will not decrypt the key in the git-repo.

WARNING:
Always check you do not commit the decrypted key!

TODO:
Find out why ansible is not setting sshkey
