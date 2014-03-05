OS X iproxy LaunchAgent
=======================

sudo port install usbmuxd

cat >> ~/.ssh/config << EOF
Host iphone
    UserKnownHostsFile /dev/null
    StrictHostKeyChecking no
    Port 5000
    User root
EOF
    
echo '127.0.0.1	localhost iphone' >> /etc/hosts

ssh-keygen

ssh iphone 'umask 077; test -d .ssh || mkdir .ssh ; cat >> .ssh/authorized_keys' < ~/.ssh/id_rsa.pub
ssh mobile@iphone 'umask 077; test -d .ssh || mkdir .ssh ; cat >> .ssh/authorized_keys' < ~/.ssh/id_rsa.pub
