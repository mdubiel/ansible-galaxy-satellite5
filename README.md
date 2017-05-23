Role Name
=========

This is an Ansible module (not a role) integrating Ansible tasks with Red Hat Satellite 5 / Spacewalk XMLRPC API

Requirements
------------

This module requires those things to work:
  - Ansible > 2.2
  - Network access to Red Hat Satellite or Spacewalk RPCXML
  - User credentials with appropriate privileges in Red Hat Satellite 5

Modul supports only Red Hat Satellite 5 not 6!

Tested on Red Hat Satellite 5.7

Dependencies
------------

python-json

Example Playbook
----------------

Available options:

 endpoint: URL to /rpc/api of your Satellite 5 instance
 username: privileged username
 password: user's password
 method: name on method listed in Red Hat Satellite 5 documentation [1]
 arguments: a list of arguments in exact order as decribed in documentation [1]
 use_session_key: if yes, internal session key will be injected to arguments list

[1] https://access.redhat.com/documentation/en-US/Red_Hat_Satellite/5.7/pdf/API_Guide/Red_Hat_Satellite-5.7-API_Guide-en-US.pdf

Task should be delegated to localhost or any other with network access to Satellite.

Invoke a 'satellite5' task:

Example 1:

list available Errata in Software Channel

- name: "List errata for Software Channel."
  satellite5:
    endpoint: "https://satellite.example.com/rpc/api"
    username: "admin"
    password: "secret"
    method: channel.software.listErrata
    arguments: [ "software_channel_1" ]
    use_session_key: yes
  delegate_to: localhost

Example 2:

Merge all Errata from Software Channel A to Software Channel B

- name: "Merge all errata from channel A to B"
  satellite5:
    endpoint: "https://satellite.example.com/rpc/api"
    username: "admin"
    password: "secret"
    method: channel.software.mergeErrata
    arguments: [ "channel_a", "channel_b" ]
    use_session_key: yes
  delegate_to: localhost


License
-------

BSD

Author Information
------------------

Mateusz Dubiel, <mdubiel@gmail.com>