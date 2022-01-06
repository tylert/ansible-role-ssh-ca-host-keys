SSH CA Host Keys Role
=====================

Stuff junk in /etc/ssh/sshd_config.d/ when adding the HostCertificate config
and HostKey values.

The user module has built-in support for creating keys for users.  The keypair
module now has the ability to set a passphrase.  SSH config module can set
config for an individual user.

Variables::

    %YAML 1.2
    ---

    delta_ssh_keys:

      - { path: /tmp/host_ca_ed25519_key, type: ed25519 }
      - { path: /tmp/user_ca_rsa_key, type: rsa, size: 4096 }

      - path: /tmp/purple_ssh_host_ed25519_key
        type: ed25519  # ed25519 keys don't care about size/bits
        comment: root@purple

      - path: /tmp/magenta_ssh_host_ed25519_key
        type: ecdsa
        size: 521  # ecdsa keys may only be 256, 384 or 521 bits
        comment: root@magenta

      - path: /tmp/blue_ssh_host_ecdsa_key
        type: dsa
        size: 1024  # dsa keys may only be 1024 bits
        comment: root@blue

    delta_ssh_certs:

      - path: /tmp/purple_ssh_host_ed25519_key-cert.pub
        public_key: /tmp/purple_ssh_host_ed25519_key.pub
        signing_key: /tmp/host_ca_ed25519_key
        type: host
        valid_from: -5m  # 5 minutes ago
        valid_to: +403d  # 365+30+7+1 days from now
        identifier: purple
        principals: purple,router01

      - path: /tmp/magenta_ssh_host_ed25519_key-cert.pub
        public_key: /tmp/magenta_ssh_host_ed25519_key.pub
        signing_key: /tmp/host_ca_ed25519_key
        type: host
        valid_from: -5m  # 5 minutes ago
        valid_to: +403d  # 365+30+7+1 days from now
        identifier: magenta
        principals: magenta,printer02

* https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html
* https://docs.ansible.com/ansible/latest/collections/community/crypto/docsite/guide_ownca.html
* https://docs.ansible.com/ansible/latest/user_guide/playbooks_delegation.html
* https://docs.ansible.com/ansible/latest/collections/community/general/ssh_config_module.html
* https://gist.github.com/kawsark/a9443692a9e4a7b1c7df253995ce864c
* https://www.acritelli.com/blog/ansible_certificate_ssh/
* https://github.com/ansible-collections/community.crypto/issues/96#issuecomment-701578598
