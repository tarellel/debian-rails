# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrant version
Vagrant.require_version '>= 1.6.0'

Vagrant.configure("2") do |config|
  config.vm.box = "chef/debian-7.6"

  # Port forward for rails app on localhost:3000
  config.vm.network :forwarded_port, guest: 3000, host: 3000
  # Port forward to http/nginx on localhost:8080
  config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # If true, then any SSH connections made will enable agent forwarding.
  # Default value: false
  config.ssh.forward_agent = true

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  #config.vm.synced_folder '.', '/vagrant', :disabled => false

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  config.vm.provider "virtualbox" do |vb|
  #   # Don't boot with headless mode
  #   vb.gui = true
  #   # Use VBoxManage to customize the VM. For example to change memory:
     vb.customize ["modifyvm", :id, "--memory", "512"]
  end
  #
  # View the documentation for the provider you're using for more
  # information on available options.



  # http://quyennt.com/system-admin/using-vagrant-ansible-to-automate-development-environment-part-2/
  # config.vm.hostname = "[hostname]" => VM's hostname, will appear as vagrant@[hostname]
  config.vm.hostname = "testbox"

  # Allow caching to be used (see the vagrant-cachier plugin)
  if Vagrant.has_plugin?("vagrant-cachier")
    config.cache.scope = :machine # :machine or :box
    #config.cache.synced_folder_opts = { type: :nfs }
    #config.cache.synced_folder_opts = {
    #  type: :nfs,
      # The nolock option can be useful for an NFSv3 client that wants to avoid the
      # NLM sideband protocol. Without this option, apt-get might hang if it tries
      # to lock files needed for /var/cache/* operations. All of this can be avoided
      # by using NFSv4 everywhere. Please note that the tcp option is not the default.
    #  mount_options: ['rw', 'vers=3', 'tcp', 'nolock']
    #}
    config.cache.auto_detect = false
    config.cache.enable :apt
    config.cache.enable :gem
    #config.cache.enable :npm
  end


  # DOCS: http://docs.ansible.com/
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provision/playbook.yml"

    # https://stackoverflow.com/questions/20952689/ansible-ssh-forwarding-doesnt-seem-to-work-with-vagrant/22768453#22768453
    ansible.host_key_checking = false
    ansible.extra_vars = { ansible_ssh_user: 'vagrant',
                 ansible_connection: 'ssh',
                 ansible_ssh_args: '-o ForwardAgent=yes'}

    # https://stackoverflow.com/questions/20952689/ansible-ssh-forwarding-doesnt-seem-to-work-with-vagrant/23704069#23704069
    # https://github.com/protobox/protobox/issues/78
    #ansible.raw_ssh_args = ['-o UserKnownHostsFile=/dev/null']
    #ansible.verbose  = 'v'
  end
end
