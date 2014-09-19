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
