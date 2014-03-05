OS X iproxy LaunchAgent
=======================

Install USB Multiplex Daemon

    sudo port install usbmuxd

-

Add iphone to hosts file

    echo '127.0.0.1	localhost iphone' >> /etc/hosts

-

Add iphone to ssh_config

    cat >> ~/.ssh/config << EOF
    Host iphone
        UserKnownHostsFile /dev/null
        StrictHostKeyChecking no
        Port 5000
        User root
    EOF

-
    
Generate ssh key

    ssh-keygen

-

Add ssh key to iPhone

    ssh iphone 'umask 077; test -d .ssh || mkdir .ssh ; cat >> .ssh/authorized_keys' < ~/.ssh/id_rsa.pub
    ssh mobile@iphone 'umask 077; test -d .ssh || mkdir .ssh ; cat >> .ssh/authorized_keys' < ~/.ssh/id_rsa.pub
