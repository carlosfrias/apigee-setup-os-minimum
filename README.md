Apigee Setup OS Minimum
=========

This roles setups the minimum operating system packages and configs that would allow OPDK to function properly. This is
a bare bones setup that can be considered a starting point but by no means the full OS setup. 

Requirements
------------

The installation of Apigee OPDK requires root access as does the installation of the system updates that are the focus 
of this role. Credentials must also be supplied to override the empty placeholders provided here. It is recommended that 
credentials be consolidated into a single credentials.yml file that can be stored separately. It is assumed that files 
containing credentials are stored in the ~/.apigee folder. 


Role Variables
--------------

| Variable Name | Default Value | Description |
| --- | --- | --- |
| apigee_continue_on_warning | y | Defaults for internal environment OPDK setup settings |
| vm_swappiness | 60 | Default value to limit swap file use |
| epel_ol6 | https://dl.fedoraproject.org/pub/epel/epel-release-latest-6.noarch.rpm | Default epel repo for EL 6 |
| epel_rhel7 | https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm | Default epel repo for EL 7 |
| yum_packages | - bind-utils
                 - chkconfig
                 - curl
                 - tar
                 - wget
                 - yum-utils
                 - unzip
                 - rsync
                 - which
                 - libselinux-python
                 - nss
                 - openssh-clients
                 - openssh-server
                 - grep
                 - rpm
                 - rng-tools
                 - sed | Collection of yum package names to install with yum |
| sysctl_minimum | 
- { name: 'vm.swappiness', value: "{{ vm_swappiness }}" }
- { name: 'net.ipv6.conf.all.disable_ipv6', value: '1' }
- { name: 'net.ipv6.conf.default.disable_ipv6', value: '1' }
- { name: 'net.ipv4.tcp_fin_timeout', value: "{{ apigee_net_ipv4_tcp_fin_timeout }}" }
- { name: 'vm.max_map_count', value: '{{ apigee_max_map_count }}' } | Minimum updates to sysctl for an Apigee node |                 

Dependencies
------------

No dependencies

Example Playbook
----------------

    - hosts: servers
      roles:
         - { role: apigee-opdk-setup-os-minimum }

License
-------

Apache License Version 2.0, January 2004

Author Information
------------------

Carlos Frias
<!-- BEGIN Google Required Disclaimer -->

# Not Google Product Clause

This is not an officially supported Google product.
<!-- END Google Required Disclaimer -->