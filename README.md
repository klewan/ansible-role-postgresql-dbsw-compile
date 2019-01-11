Ansible Role: postgresql-dbsw-compile
=====================================

This role is used for PostgreSQL source code compliation.

Supported OS:
-------------
* RedHat
* CentOS
* OracleLinux

Requirements
------------

None

Role Variables
--------------

Available variables are listed below, along with default values (see `defaults/main.yml`):

    #
    # Software distribution
    #

    # Software location
    postgresql_dbsw_compile_sw_source_db:
      - { filename: /software/postgres/source/postgresql-9.6.10.tar.gz, version: 9.6.10 }

    # whether or not 'postgresql_dbsw_compile_sw_source_db' is available remotely via NFS
    postgresql_dbsw_compile_sw_remote_src: no

    # location where compiled binaries will be stored
    postgresql_dbsw_compile_sw_binary_packages_directory: "{{ postgresql_binary_packages_directory | default('/software/postgres/binary', true) }}"

    # owner of binaries stored in 'postgresql_dbsw_compile_sw_binary_packages_directory'
    postgresql_dbsw_compile_sw_binary_packages_directory_owner: postgres

    # directory where source code files will be copied to
    postgresql_dbsw_compile_compile_directory: "{{ postgresql_pghomes_directory }}/compile"

    # packages required for PostgreSQL source compilation
    postgresql_dbsw_compile_required_packages:
      - gcc
      - openldap-devel
      - python-devel
      - readline-devel
      - redhat-lsb
      - bison
      - flex
      - perl-ExtUtils-Embed
      - zlib-devel
      - crypto-utils
      - openssl-devel
      - pam-devel
      - libxml2-devel
      - libxslt-devel
      - tcl
      - tcl-devel
      - openssh-clients
      - bzip2
      - net-tools
      - wget
      - screen
      - unzip
      - sysstat
      - xorg-x11-xauth

    # extra flags used with compile command
    postgresql_dbsw_compile_flags_extra:
      with-pgport: 5432
      with-perl:
      with-python:
      with-openssl:
      with-pam:
      with-ldap:
      with-libxml:
      with-libxslt:
      with-extra-version: '" {{ postgresql_pghomes_binary_prefix|upper }} compiled PostgreSQL"'
      with-wal-segsize: 64
      with-blocksize: 8
      with-segsize: 2
	  

Dependencies
------------

This role uses `postgresql` role.

Example Playbook
----------------

    - name: Compile PostgreSQL database server software
      hosts: pg-servers
      become: true
      become_user: '{{ postgresql_user }}'
      roles:
        - { role: postgresql-dbsw-compile, tags: postgresql-dbsw-compile }

Inside `vars/main.yml` or `group_vars/..` or `host_vars/..`:

    #----------------------------------------------------
    # overrides role 'postgresql-dbsw-compile' variables
    #----------------------------------------------------

    # Software location
    postgresql_dbsw_compile_sw_source_db:
      - { filename: /software/postgres/source/postgresql-9.6.10.tar.gz, version: 9.6.10 }

    # whether or not 'postgresql_dbsw_compile_sw_source_db' is available remotely via NFS
    postgresql_dbsw_compile_sw_remote_src: no

    # location where compiled binaries will be stored
    postgresql_dbsw_compile_sw_binary_packages_directory: /software/postgres/binary

    # owner of binaries stored in 'postgresql_dbsw_compile_sw_binary_packages_directory'
    postgresql_dbsw_compile_sw_binary_packages_directory_owner: postgres

    # extra flags used with compile command
    postgresql_dbsw_compile_flags_extra:
      with-pgport: 5432
      with-perl:
      with-python:
      with-openssl:
      with-pam:
      with-ldap:
      with-libxml:
      with-libxslt:
      with-extra-version: '" {{ postgresql_pghomes_binary_prefix|upper }} compiled PostgreSQL"'
      with-wal-segsize: 64
      with-blocksize: 8
      with-segsize: 2

    # ... etc ...


License
-------

GPLv3 - GNU General Public License v3.0

Author Information
------------------

This role was created in 2018 by [Krzysztof Lewandowski](mailto:Krzysztof.Lewandowski@fastmail.fm).


