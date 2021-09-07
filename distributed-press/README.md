# Prepearing a server
- Debian 11
- user capable of sudo
```
apt-get install sudo
/usr/sbin/usermod -aG sudo [USER]
```
- passwordless sudo enabled
```
sudo sed -i 's/ALL=(ALL:ALL) ALL/ALL=(ALL:ALL) NOPASSWD:ALL/' /etc/sudoers
```
- Public key form ansible host copied to target host

# Adding a server to Ansible

1. Add new server into inventory under `[webserver]` with the line
```
<servername> ansible_host=<ipaddress>  ansible_ssh_user=<username>
```
For example for a server called `test-server` on ip address `192.168.1.5` with user account of `user`

```
test-server ansible_host=192.168.1.5  ansible_ssh_user=user
````

2. Create a folder `host_vars/<servername>`

3. Create configuration file `var.yml` with the following content

Sample config:
```
---
dpress_config_name: blank
ipv6_admin_subs:
  - ::/0
ipv4_admin_subs:
  - 0.0.0.0/0
dat_username: nopassword
dat_password: nopassword
letsencrypt_enable: false
letsencrypt_staging: false
domain_name: distributedpress.local
```

4. Run ansible playbook

`ansible-playbook -i inventory --limit <servername> deploy-server.yml`

# Configuration

**domain_name:** Name of top level domain. Will prepent api,ipfs,hyper  as needed

**dpress_config_name:**  Filename of configuration file for the API. `config<dpress_config_name>.json`. `blank` will create an empty json file.

**ipv6_admin_subs**,**ipv4_admin_subs**: IP subjects that you will be allowed to SSH into from.

**dat_username**,**dat_password:** Hypercore login and password

**letsencrypt_enable:** Generate Lets Encrypt certificate (`true`) or use Self Signed certificate (`false`). Running localy you should set this to false. `true` if device has a real-world domain server and accessable via the internet.

**letsencrypt_staging:** When using Lets Encrypt, create staging certificate (true) or production certificate (false). Staging certificate will not pass browser checks and will throw an error. Production certificates are throttled.