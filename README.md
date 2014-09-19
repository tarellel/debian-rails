## Requirements

[Vagrant](http://www.vagrantup.com/) and [Ansible](http://docs.ansible.com/index.html)

    brew install ansible
    (ansible > 1.3, and it's dependencies)

This ansible build works best with using [Debian](https://www.debian.org/) images/boxes.


[Config and Setup of Vagrant](https://gist.github.com/dergachev/3866825)

### Before Running ###

copy id_rsa.pub to the files directory, because ssh is changed to use pubkey authentication.

    cp ~/.ssh/id_rsa.pub provision/files/workstation.pub


To use with [DigitalOcean](https://www.digitalocean.com/) use the following commands:
    # https://github.com/smdahlen/vagrant-digitalocean
    vagrant plugin install vagrant-digitalocean

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

    Copy contents of file or change from DigitalOcean to Vagrantfile in base directory

    # to load it up use the following command
    vagrant up --provider=digital_ocean

    # reprovision the
    vagrant provision



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




## Various Sources

* [hardining-wheezy](https://github.com/deptadapt/ansible-wheezy)
* [deptadapt/ansible-wheezy](https://github.com/deptadapt/ansible-wheezy/tree/master/roles)
* [hostmaster/ansible-digitalocean-bootstrap](https://github.com/hostmaster/ansible-digitalocean-bootstrap)


* [eduardodeoh/ansible](https://github.com/eduardodeoh/ansible)
* [protobox/protobox](https://github.com/protobox/protobox/tree/master/lib/ansible/roles)
* [owainlewis/vagrant-ansible-rails](https://github.com/owainlewis/vagrant-ansible-rails)
* [M4nu/ansible](https://github.com/M4nu/ansible)

### Major Inspiration ###
* [bedrock-ansible](https://github.com/roots/bedrock-ansible)
* [the-ansibles](https://github.com/pjan/the-ansibles)
* [sovereign](https://github.com/al3x/sovereign)
* [vlad](https://bitbucket.org/philipnorton42/vlad/src/8946cdde019e0ed3f9d9e53b069906dad4b879bd?at=master)
* [statserver](https://github.com/DandyDev/statserver)

#### Jumble
* [CenterForOpenScience/cos-ansible-base](https://github.com/CenterForOpenScience/cos-ansible-base)
* [jcftang/ansible-hydra](https://github.com/jcftang/ansible-hydra)
* [M4nu/ansible](https://github.com/M4nu/ansible)
* [CenterForOpenScience/cos-ansible-base](https://github.com/CenterForOpenScience/cos-ansible-base)
* [Mini mix](https://github.com/sfromm/ansible-playbooks)
* [hnakamur/ansible-playbooks](https://github.com/hnakamur/ansible-playbooks/tree/master/roles)
* [ryankanno/ansible-roles](https://github.com/ryankanno/ansible-roles)
* [pvillega/ansible-ec2-play](https://github.com/pvillega/ansible-ec2-play)

### Rails based ###
* **UFW** [ansible-ubuntu-rails-server](https://github.com/jbinto/ansible-ubuntu-rails-server)
* [ansible-ubuntu-rails-nginx-puma](https://github.com/tobyhede/ansible-ubuntu-rails-nginx-puma)
* [https://github.com/tilsammans/playbook](https://github.com/tilsammans/playbook)
* [eduardodeoh/ansible](https://github.com/eduardodeoh/ansible/tree/master/)
* [slickage/ansible-rails](https://github.com/slickage/ansible-rails)
* [alvinsj/digitalocean-ansible-rails](https://github.com/alvinsj/digitalocean-ansible-rails)
* [jbinto/ansible-ubuntu-rails-server](https://github.com/jbinto/ansible-ubuntu-rails-server)
* [nickjj/ansible-rails](https://github.com/nickjj/ansible-rails)

### nginx & Rails ###
* [mortik/ansible-nginx-rails](https://github.com/mortik/ansible-nginx-rails)
* [zealot128/ansible-rails_apps](https://github.com/zealot128/ansible-rails_apps)
* [dpausp/ansible-playbook-redmine](https://github.com/dpausp/ansible-playbook-redmine)


#### nginx w/SSL
* [dpausp/ansible-playbook-redmine](https://github.com/dpausp/ansible-playbook-redmine/blob/master/playbook-redmine/roles/redmine/tasks/nginx.yml)


### DigitalOcean Provisions
* [from-zero-to-deploymeny](http://ihassin.wordpress.com/2013/12/30/from-zero-to-deployment-vagrant-ansible-capistrano-3-to-deploy-your-rails-apps-to-digitalocean-automatically-part-2/)
* [alvinsj/digitalocean-ansible-rails](https://github.com/alvinsj/digitalocean-ansible-rails)


##### rbenv
* [leucos/ansible-rbenv-playbook](https://github.com/leucos/ansible-rbenv-playbook)
* [mmoya/ansible-playbooks](https://github.com/mmoya/ansible-playbooks/blob/master/rbenv/main.yml)
* [https://github.com/jeffersongirao/deploying_rails_with_ansible/blob/master/provisioning/app_server.yml](https://github.com/jeffersongirao/deploying_rails_with_ansible/blob/master/provisioning/app_server.yml)



## Linux Modules

### fail2ban
* **!!!** [ansible-security](https://github.com/nickjj/ansible-security)
* [ansible-fail2ban](https://github.com/nickjj/ansible-fail2ban)


### ufw
* [ansible-ufw](https://github.com/jlund/ansible-ufw)

### Important Posts
* [Understandable Provisioning](http://julien.ponge.org/blog/scalable-and-understandable-provisioning-with-ansible-and-vagrant/)
* [Install Ansible, Create Your Inventory File](http://thornelabs.net/2014/03/08/install-ansible-create-your-inventory-file-and-run-an-ansible-playbook-and-some-ansible-commands.html)
* [Setup dev env in vagrant w/ rvm pg rails nginx unicorn](https://coderwall.com/p/gmlv_w)
* [10_new_roles_when_combined_together_fully/](http://www.reddit.com/r/ansible/comments/26tlv4/10_new_roles_when_combined_together_fully/)

##### NGINX w/Rails
* [Launch Rails 4 application with passenger and nginx](http://alexbachuk.com/launch-rails-4-application-with-passenger-and-nginx/)


##### RVM
* [Installing Ruby with RVM on Ubuntu 12.04 Server ](http://renaud-cuny.com/en/blog/2013-04-11-step-by-step-ruby-rvm-installation-ubuntu-server/)

### To Install Test packages
    # src: http://www.binarytides.com/enable-testing-repo-debian/
    # View available installs of a package
    apt-cache policy lynis

    # Method 1
    apt-get install lynis/testing

    Method 2
    apt-get -t testing install lynis



### View List of open ports
    sudo lsof -i
    sudo netstat -lptu
    sudo netstat -tulpn
    netstat -lntu


#### View list of BLocked ports/Firewalled
    # To view status of UFW do the following command
    sudo ufw status
    sudo ufw status verbose


#### Phusion Passenger Commands
    sudo passenger-status
    sudo passenger-memory-stats


#### Connect to postgresql
    sudo su postgres
    psql --username={{ db_username }} --dbname={{ app }} --host=localhost


#### Get Security Audit Results
    # do a security audit
    sudo lynis -c --auditor "{{ admin }}"
    sudo lynis --check-all -c -Q
    sudo lynis -c -Q --auditor "{{ admin/user }}"

    # do a system rootkit scan
    sudo rkhunter -c --enable all --disable none
    sudo rkhunter -c

    #  to run chkrootkit [rootkit scan]
    sudo chkrootkit


#### System Monitoring
    htop


##### Misc
    sudo chmod user:group dirctoryOrFile
    sudo chmod -R user:group dirctory # changes owner of directory and all of its contents [recursive]

    # Stay root
    sudo -i

    # Verify sshd_config
    /usr/sbin/sshd -t

    # Get Postfix
    sudo postfix status

    # Get server request information
      # https://www.digitalocean.com/community/tutorials/how-to-configure-varnish-cache-4-0-with-ssl-termination-on-ubuntu-14-04
    curl -I localhost:8080

    # Benchmark Redis
    redis-benchmark -q -n 100000 -c 50 -P 12

    # Begin resque workers
    TERM_CHILD=1 QUEUES=* rake resque:work
    # Deprecated: COUNT=8 QUEUE=* rake resque:workers
    COUNT=2 QUEUES=* rake resque:work
    rake resque:workers COUNT=2 QUEUE=*
    rake resque:workers


    ##### User management
    # verify number of users login attempts
    pam_tally2 -u username
    # to release locked user from login attempts
    pam_tally2 -r -u username


    #Passenger (force start|stop)
    sudo passenger start
    sudo passenger stop


#### Port Knocking
    # required: brew install knock
    knock -v IPaddress 7000 8000 9000


#### Fail2ban
    # fail2ban status
    sudo fail2ban-client status
    sudo fail2ban-client status <module>

    #View list of banned IP addresses - http://www.the-art-of-web.com/system/fail2ban-log/
    awk '($(NF-1) = /Ban/){print $NF}' /var/log/fail2ban.log | sort | uniq -c | sort -n

    # Group by IP address and Fail2ban section
    grep "Ban " /var/log/fail2ban.log | awk -F[\ \:] '{print $10,$8}' | sort | uniq -c | sort -n


    ----- Not working
    # Remove [invalid method]
    sudo iptables -D fail2ban-mmonit -s 192.168.0.1 -j DROP

    # http://blog.shanghai-hosting.com/2013/10/tech-how-to-unban-an-ip-address-from-your-server-using-fail2ban/
    sudo fail2ban-client get jail-name actionunban ipaddress
    sudo fail2ban-client get mmonit actionunban 10.0.2.2


    # get list of banned with iptables
    iptables -L -n
