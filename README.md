rm.cowrie
=========

A role that sets up cowrie honeypot on a target system.
This creates a new user, clones cowrie into its' homefolder and installs all needed dependencies in a venv in the cowrie homefolder.

Requirements
------------

The role assumes that the SSH server has been moved from port 22, as it is setting up iptables forwards for port 22 and 23. This behaviour can be disables by setting `cowrie_redirect_ports: no` - then cowrie will be reachable by port 2222 and 2223 only.

Role Variables
--------------

In general, the config can be edited in great detail. I would recommend that you change at least some vars to prevent fingerprinting.
The ttylog, which records all entered commands of a session in UML, has been disabled to save disk space. This can be activated again.
```
  - cowrie_hostname -> Sets the displayed hostname
  - cowrie_version_string -> This version string is presented at the SSH banner
  - cowrie_ttylog -> Set to true to enable logging
```

Dependencies
------------

None! :)

Example Playbook
----------------

If only the recommended vars are set, deploying cowrie is really easy:

    - hosts: servers
      roles:
        - role: rm.cowrie
          vars: 
            cowrie_hostname: derp04
            cowrie_version_string: SSH-2.0-OpenSSH_6.0p1 Debian-4+deb7u2

If you want to change the default allowed users on your honeypot, modify `templates/userdb.txt`.

License
-------

Apache