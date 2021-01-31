# Service Loomio

The `deploy-loomio.yml` playbook will provision a virtual machine and setting up Loomio with default configuration.

To deploy run the following command:
```
ansible-playbook -i inventory deploy-loomio.yml --ask-vault-pass
```