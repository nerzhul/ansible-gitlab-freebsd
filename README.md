gitlab-freebsd
=========

This role install a complete gitlab instance under FreeBSD

Requirements
------------

* FreeBSD host or jail which has access to a FreeBSD repository (official, or custom, look at the installed packages in the role)
* FreeBSD 9.1 or greater (pkgng is required)
* Nginx web server on the gitlab host
* Redis server (on the gitlab host, or not)
* PostgreSQL 9.2 or greater (on the gitlab host, or not)
* A PostgreSQL database for gitlab with a dedicated user & host

Role Variables
--------------

Available variables are listed below, along with default values:

```
---
gitlab:
  user: git
  uid: 7500
  group: git
  gid: 7500
  version: 8-4-stable
  host: gitlab.local
  home: /home/git
  http_ssl: true
  http_ipv6: true
  mail: gitlab@gitlab.local
  mail_reply_to: no-reply@gitlab.local
  secret_key: myfabuloussecretkey
  redis:
    host: 127.0.0.1
    port: 6379
  db:
    name: gitlabdb
    user: gitlab
    password: gitlabpwd
    host: 127.0.0.1
    port: 5432
  lfs_enable: false
  path:
    datadir: "/var/db/gitlab"
    repositories: "{{ gitlab.path.datadir }}/git-repositories"
    lfs_objects: "{{ gitlab.path.datadir }}/lfs-objects"
    logs: "/var/log/gitlab"
  unicorn:
    mem_min: 300
    mem_max: 350
  ldap:
    enable: false
    host: 127.0.0.1
    port: 389
    attr_uid: "uid"
    base: "ou=people,dc=example,dc=org"
    method: "plain"
    bind_dn: "cn=ro-user,dc=example,dc=org"
    bind_password: "ro-user_password"
    is_activedirectory: false
    block_auto_created_users: false
  omniauth:
    enable: false
    block_auto_created_users: true
    github:
      app_id: false
      app_secret: false
    twitter:
      app_id: false
      app_secret: false
```

Dependencies
------------

Nothing

Example Playbook
----------------

    - hosts: gitlabhost
      vars_files: vars/gitlab_custom.yml
      roles:
         - gitlab-freebsd


Post installation
-----------------

* Include /usr/local/etc/nginx/gitlab.conf in your /usr/local/etc/nginx/nginx.conf

License
-------

BSD

Author Information
------------------

Created by Loic Blot <loic.blot@unix-experience.fr> (http://www.unix-experience.fr)
