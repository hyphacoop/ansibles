# Deploy Hypha sites

To deploy websites we first need to provision `bw1` (backend web server 1) which will host our websites.

For `staging` environment depoy by running this command:
```
ansible-playbook -i inventory_staging --ask-vault-pass deploy-server-bw1.yml --extra-vars "staging_env=true"
```

For `production` environment depoy by running this command:
```
ansible-playbook --ask-vault-pass deploy-server-bw1.yml
```
---
The following playbooks are optional and can be provisioned in any order.
The playbooks will first configure `bw1` with the directory where website files are stored, after it will configure the frontend web server to reverse proxy to the new sites.

After the playbook successfully deployed you will need to force a build on Travis CI to upload the website files to `bw1`.

`deploy-site-hypha.coop.yml` deploys [hypha.coop](https://hypha.coop)
Staging: `ansible-playbook -i inventory_staging deploy-site-hypha.coop.yml --extra-vars "staging_env=true"`
Production: `ansible-playbook deploy-site-vision.hypha.coop.yml`

`deploy-site-link.hypha.coop.yml` deploys [link.hypha.coop](https://link.hypha.coop)
Staging: `ansible-playbook -i inventory_staging deploy-site-link.hypha.coop.yml --extra-vars "staging_env=true"`
Production: `ansible-playbook  deploy-site-link.hypha.coop.yml`

`deploy-site-vision.hypha.coop.yml` deploys [vision.hypha.coop](https://vision.hypha.coop)
Staging: `ansible-playbook -i inventory_staging deploy-site-vision.hypha.coop.yml --extra-vars "staging_env=true"`
Production: `ansible-playbook deploy-site-vision.hypha.coop.yml`
