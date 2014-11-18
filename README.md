Stouts.nginx
============

[![Build Status](http://img.shields.io/travis/Stouts/Stouts.nginx.svg?style=flat-square)](https://travis-ci.org/Stouts/Stouts.nginx)
[![Galaxy](http://img.shields.io/badge/galaxy-Stouts.nginx-blue.svg?style=flat-square)](https://galaxy.ansible.com/list#/roles/854)

Ansible role which simple manage nginx

* Install and upgrade;
* Provide hanlers for restart and reload;
* Support simple site configurations.

#### Variables

```yaml
nginx_enabled: yes                  # The role in enabled
nginx_dir: /etc/nginx               # Nginx config directory
nginx_sites_dir: "{{nginx_dir}}/sites-enabled" # Nginx include directory
nginx_default_site: "{{nginx_sites_dir}}/default"
nginx_delete_default_site: no
nginx_user: www-data                # -------------------
nginx_worker_processes: 4           #   See nginx docs
nginx_worker_connections: 1024      # -------------------
nginx_sendfile: yes
nginx_keepalive_timeout: 65
nginx_gzip: yes
nginx_server_names_hash_bucket_size: 128
nginx_access_log: /var/log/nginx/access.log
nginx_error_log: /var/log/nginx/error.log
nginx_http_options:                 # Additional http options (each line will be added as is)
                                    # Ex: nginx_http_options:
                                    #       - auth_basic "You shall not pass!";
                                    #       - auth_basic_user_file {{nginx_auth_file}};

nginx_servers:                      # Setup servers (simplest interface, use cfg files for large configurations)
                                    # Ex: nginx_servers:
                                    #     - |
                                    #       listen 80;
                                    #       server_name localhost;
                                    #       location / { root html; index index.html; }
                                    #     - |
                                    #       listen 80;
                                    #       server_name test.com;
                                    #       location / { root /test; index index.html; }

nginx_auth_file: "{{nginx_dir}}/.htpasswd" # Where stored passwords
nginx_auth_users: []                # Setup users for http authentication
                                    # nginx_auth_users:
                                    #   - { name: team, password: secret }

nginx_status: 127.0.0.1             # Report about nginx state by IP. Set empty for disable.
```

#### Usage

Add `Stouts.nginx` to your roles and set vars in your playbook file.

Example:

```yaml

- hosts: all

  roles:
    - Stouts.nginx

  vars:
    nginx_servers:
    - |
      listen 80;
      server_name google.com;
      location / { root /var/www/google; index index.html; }
```

#### License

Licensed under the MIT License. See the LICENSE file for details.

#### Feedback, bug-reports, requests, ...

Are [welcome](https://github.com/Stouts/Stouts.nginx/issues)!
