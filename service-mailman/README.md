# Service mailman

The `deploy-mailman.yml` playbook will provision a virtual machine and setting up mailman with default configuration.

To deploy run the following command:
```
ansible-playbook -i inventory deploy-mailman.yml --ask-vault-pass
```