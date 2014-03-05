OS X iproxy LaunchAgent
=======================

Install USB Multiplex Daemon

    sudo port install usbmuxd

-

Download Agent start script

    curl https://raw.github.com/emergy/LaunchAgents/master/org.usbmuxd.iproxy.plist > ~/Library/LaunchAgents/org.usbmuxd.iproxy.plist

-

Add start script to launchd

    launchctl load -w $HOME/Library/LaunchAgents/org.usbmuxd.iproxy.plist

-

Start iproxy

    launchctl start org.usbmuxd.iproxy

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
