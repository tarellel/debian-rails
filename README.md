## Requirements

[Vagrant](http://www.vagrantup.com/) and [Ansible](http://docs.ansible.com/index.html)

    brew install ansible
    (ansible > 1.3, and it's dependencies)

This ansible build works best with using [Debian](https://www.debian.org/) images/boxes.


[Config and Setup of Vagrant](https://gist.github.com/dergachev/3866825)

### Before Running ###

copy id_rsa.pub to the files directory, because ssh is changed to use pubkey authentication.

    cp ~/.ssh/id_rsa.pub provision/files/workstation.pub



##### Required steps

    # vagrant plugins - https://github.com/mitchellh/vagrant/wiki/Available-Vagrant-Plugins
    # vagrant caching - https://github.com/fgrehm/vagrant-cachier
    #   http://fgrehm.viewdocs.io/vagrant-cachier
    #   https://github.com/fgrehm/vagrant-cachier/blob/master/docs/usage.md
    vagrant plugin install vagrant-cachier

    ########## START ##########
    # Depending on your setup you may need to issue the following commands
    # you more than likely won't need to use the following commands
    ##########
    brew install curl-ca-bundle
    #add the following line to you environment file .bashrc .zshrc .bash_profile etc
    export SSL_CERT_FILE=/usr/local/opt/curl-ca-bundle/share/ca-bundle.crt
    ########## END ##########




## Vagrant Commands ##

Load and Provision the Box/VM

    vagrant up


Reload and (re)Provision the box

    vagrant reload --provision


Shutdown/Suspend the current VM

    vagrant halt
    vagrant suspend


Completely Destroy the provisioned box/VM

    vagrant destroy
    # destroy vagrant VM without confirmation
    vagrant destroy -f

    # if vagrant/ansible freezes giving you an error that the instance is already open use the following commands
    vagrant global-status
    # this will output all open vagrant instances with their ids, providers etc
    vagrant destroy 0965180
    # this will kill the current vagrant process with that particular specified id


#### DigitalOcean
To use with [DigitalOcean](https://www.digitalocean.com/) use the following commands:

    # https://github.com/smdahlen/vagrant-digitalocean
    vagrant plugin install vagrant-digitalocean

    Copy contents of file or change from host_vagrants/digitalocean to Vagrantfile in base directory

    # to load it up use the following command
    vagrant up --provider=digital_ocean

    # reprovision the VM
    vagrant provision



### Vagrant Roles ###

| Role | Contents |
| --- | --- |
| apt | Update and upgrade |
| build | Install and build required libraries |
| database | Install redis, PostgreSQL, and databases |
| development | Install all general required tools (imagemagick, memcached, etc.)|
| prereq_config | Configure Prerequisites for particular settings in order to install needed packages |
| ruby | Install Ruby, RVM, Rails |
| security | Harden Linux box, install ufw, ssh, and fail2ban |
| webserver | Install nginx, Phusion Passenger, and required libraries |
