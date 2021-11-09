SSH CA Host Keys Role
=====================

Stuff junk in /etc/ssh/sshd_config.d/ when adding the HostCertificate config
and HostKey values.

The user module has built-in support for creating keys for users.  The keypair
module now has the ability to set a passphrase.  SSH config module can set
config for an individual user.

* https://docs.ansible.com/ansible/latest/collections/community/crypto/docsite/guide_ownca.html
* https://docs.ansible.com/ansible/latest/user_guide/playbooks_delegation.html
* https://docs.ansible.com/ansible/latest/collections/community/general/ssh_config_module.html
* https://gist.github.com/kawsark/a9443692a9e4a7b1c7df253995ce864c
* https://www.acritelli.com/blog/ansible_certificate_ssh/
* https://github.com/ansible-collections/community.crypto/issues/96#issuecomment-701578598
