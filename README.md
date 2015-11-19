# Model DevOps pipeline

This project is a sandbox which I'm using to learn about DevOps tooling, and how it can be made to integrate.

## Getting Started

### One-time Prerequsites

1. You'll need a working `docker` environment, including `docker-compose` and, if required `docker-machine`. This is beyond the scope of this environment, but for Mac OS X, [homebrew](http://brew.sh) is very easy `brew install docker-compose` should do it. If not, `brew install docker-compose docker docker-machine`. Actually, you might also need VirtualBox. Windows, Linux and other more esoteric platforms are left as an exercise for the reader. Sorry.

2. I also assume you have `git`, or else how are you going to clone the repository?

3. Clone the repository with the following terminal command

        git clone https://github.com/dringtech/devops-sandbox.git

    NB If you've already cloned on github, I assume you probably realise what you need to change, you power user, you.

4. Make sure your docker-machine is created

        docker-machine create devops --driver virtualbox --virtualbox-disk-size "30000" --virtualbox-hostonly-cidr "192.168.111.1/24" --virtualbox-memory "4096"

    Feel free to change any of these settings (name, disk size, network, memory) if you feel confident to.

5. Ensure your machine can resolve the required hosts (see Hints and Tips [Service name resolution](#Service name resolution) section, below)

### Starting up

1. Make sure your docker machine is up and running

        docker-machine devops start

2. Ensure that your environment is set correctly

        eval $(docker-machine env devops)

  NB This is true for Mac OS X and Linux. Windows may differ.

3. Make sure you're in the same directory as `docker-compose.yml`.

4. Build the services

        docker-compose build

5. Go and do something which takes a reasonably long time. The `build` command is downloading the docker images and creating tailored versions. If you've got low bandwidth, this may take some time.

6. Once complete, you can start the services with

        docker-compose start

  The services will start. They may take a moment to initialise first time round.

7. You can check the status with

        docker-compose ps

  or
        docker-compose logs

  `logs` also enables you to specify individual services as defined in
  `docker-compose.yml`.

### Accessing the services

The services are published on the following urls:

* Freeipa <https://freeipa.devops/>
* GitLab <http://gitlab.devops/>
* JIRA <http://jira.devops/>
* Confluence <http://confluence.devops/>
* Jenkins <http://jenkins.devops/>

Note that the SSL certificates are self-signed, and will ask you if you wish to trust them.

There is a separate LDAP server at the moment, which GitLab is integrated with. This is not initially populated, and will need to be configured manually.

You will need to sign on to JIRA and Confluence and create / install trial licenses.

## Hints and Tips

### Service name resolution

If your platform supports it, create a resolver file. For example, Mac OS X can be configured with a `/etc/resolver/devops` file. This references the local `dnsmasq` DNS server running in docker.
Not sure if Windows can work in the same.

    nameserver 192.168.111.100

You will need to replace `192.168.111.100` with the IP address of the docker machine if you have changed the host only network address.

If you don't do this, you'll need a way of resolving the various domain names.
The simplest way to do this is to add the hosts to the `hosts` file for your
platform. Google it...

    192.168.111.100    docker gitlab.devops jenkins.devops confluence.devops jira.devops freeipa.devops

NB Other domain names won't be matched by the router, unless you edit the router sites files. If this makes no sense to you, don't do it.

### Create `.ssh/config` file

This file enables `ssh` to use a different port and sign in for each host.

    Host                gitlab.devops
        Hostname        gitlab.devops
        Port            2222
        IdentityFile    ~/.ssh/gitlab_ssh
        IdentitiesOnly  yes
