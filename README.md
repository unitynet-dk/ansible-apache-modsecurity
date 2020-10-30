# ansible-apache-modsecurity

Install and configure Apache mod_security2 module.

Ansible Role: apache-modsecurity

Ansible Role to install and configure Apache mod_security2 in Ubuntu, Debian or Red Hat based distributions.
Requirements

None.
Role Variables

Most common variables are listed below, the (mostly) immutable ones are in defaults/main.yml and the recommended settings are in var/main.yml, this last file would be the one to edit. There are also a couple of templates for the modsecurity.conf file, a minimal one and a recommended by mod_security itself.

The apache config folder for each distribution by default/main.yml:

apache_conf_dir_debian: "/etc/apache2/conf-available"
apache_conf_dir_redhat: "/etc/httpd/conf.d"

The settings in var/main.yml:

Enable mod_security in detection only mode, you should change this to On once you are sure everything is working as intended:

SecRuleEngine: DetectionOnly

Request rules:

SecRequestBodyAccess: On
SecRequestBodyLimit: 13107200
SecRequestBodyNoFilesLimit: 131072
SecRequestBodyInMemoryLimit: 131072
SecRequestBodyLimitAction: Reject
SecResponseBodyAccess: On
SecResponseBodyMimeType: "text/plain text/html text/xml"
SecResponseBodyLimit: 524288
SecResponseBodyLimitAction: ProcessPartial

Temporary and permanent data stores:

SecTmpDir: /tmp/
SecDataDir: /tmp/

Log settins:

SecAuditEngine: RelevantOnly
SecAuditLogParts: ABIJDEFHZ
SecAuditLogType: Serial
SecAuditLog: /var/log/modsec_audit.log

Share status with mod_security developers:

SecStatusEngine: On

Dependencies

Must have installed Apache. Suggested role:

geerlingguy.apache

For Red Hat and CentOS the EPEL repository is necessary:

geerlingguy.epel

Example Playbook

- hosts: all
  roles:
    - unitynet-dk.apache-modsecurity
