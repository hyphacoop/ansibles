# NGINX reverse proxy

The `deploy-nginx-reverse-proxy.yml` playbook will provision a virtual machine and configure the frontend NGINX reverse proxy for backend web servers.

For `staging` environment deploy by running this command:
```
ansible-playbook -i inventory_staging --ask-vault-pass deploy-nginx-reverse-proxy.yml --extra-vars "staging_env=true"
```

For `production` environment deploy by running this command:
```
ansible-playbook --ask-vault-pass deploy-nginx-reverse-proxy.yml
```
