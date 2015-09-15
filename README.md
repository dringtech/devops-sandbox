
# Hints and Tips

## Create `/etc/resolver/devops` file

Points at the dnsmasq server running in docker. Works in Mac OS X.

    nameserver 192.168.111.100

## Create `.ssh/config` file

This file enables `ssh` to use a different port and sign in for each host.

    Host                gitlab.devops
        Hostname        gitlab.devops
        Port            2222
        IdentityFile    ~/.ssh/gitlab_ssh
        IdentitiesOnly  yes
