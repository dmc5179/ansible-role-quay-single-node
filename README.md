#  quay-ansible

Quay Ansible
=========

This role is intended to install Quay and its dependencies on a single system using the basic installation method.

Requirements
------------

Before running:

1) Install required ansible collections

 ```
 ansible-galaxy collection install -r requirements.yml
 ```

2) Install required ansible roles

 ```
 ansible-galaxy install -r requirements.yml
 ```

3) Requires Ansible 2.7+ on the host executing these playbooks

4) You should have sufficient storage allocated to the node to hold the downloaded images. This directory is defined in the group_vars/all as the QUAY_STORAGE_DIR. Default is /opt/quay/storage.


Usage
-----

+ If this is the first time that you've installed Quay, you will need to go through the Quay configuration mode to create your config tarball. Do this by adding the following flag to the playbook `-e QUAY_CONFIG=true`

```
ansible-playbook -i hosts deploy.yml -b -e quay_config=true
```


+ If you've already run the config mode, or have a config tarball you can run the full deployment by referencing a configuration tarball. After running through the Quay config WebUI, copy the downloaded tarball to the ansible host and reference it with `-e QUAY_CONFIG_TAR=<path to tarball>`


```
ansible-playbook deploy.yml -i hosts -b -e QUAY_CONFIG_TAR=<path to quay config tarball>
```



Role Variables
--------------

Review the variables stored under group_vars/all to ensure that they align with your desired configurations. Default passwords are included here and should be changed or overwritten at run time.

## Variables:

| Variable Name  | Default | Description |
| -------------  |:-------:|:-----------:|
| clair_encrypt  | true    |             |
| clair_endpoint | "clair.dns.podman" | The FQDN for your clair server, defaults to same as quay |
| clair_image    | '' ||
| fips_enabled |  true ||
| postgresql_db | 'quay' | The postgres clair database |
| postgresql_hostname | 'postgresql-quay.dns.podman' 
| postgresql_image | ||
| postgresql_password | 'quaypass' | The postgres admin user |
| postgresql_port | 5432 | Port to access postgres on |
| postgresql_quay_db | clair | The postgres clair database |
| postgresql_quay_user_password | changeme | The postgres quay user password |
| postgresql_quay_user | quay | The postgres clair database user |
| postgresql_user | 'quayuser' ||
| quay_config_mode | false ||
| quay_config_password | changeme | The password for the quay config UI |
| quay_config_port | 8080 | The port to access the quay configuration pod |
| quay_hostname | 'quay.danclark.io' ||
| quay_http_port | 80 | The port to access Quay if TLS is not enabled |
| quay_https_port | 443 | The port to access Quay when TLS is enabled |
| quay_image |  '' | The source and tag of Quay container |
| quay_redis_deploy | true ||
| quay_root_dir | /opt/quay | The directory where quay and clair configurations will be placed |
| quay_san | '' ||
| redis_hostname | 'redis.dns.podman' ||
| redis_image | ||
| redis_password | 'strongpassword' | The password to set on deployed Redis |

Documentation generated using: [Ansible-autodoc](https://github.com/AndresBott/ansible-autodoc)
