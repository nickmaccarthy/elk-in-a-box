require 'yaml'
elk_config = YAML::load(File.read("#{File.dirname(__FILE__)}/elk.config.yaml"))

# Plugins
if ARGV[0] != 'plugin'

    # Define the plugins in an array format
    required_plugins = [
      'vagrant-vbguest', 'vagrant-hostmanager', 
      'vagrant-disksize', 'vagrant-scp'
    ]         
    plugins_to_install = required_plugins.select { |plugin| not Vagrant.has_plugin? plugin }
    if not plugins_to_install.empty?
  
      puts "Installing plugins: #{plugins_to_install.join(' ')}"
      if system "vagrant plugin install #{plugins_to_install.join(' ')}"
        exec "vagrant #{ARGV.join(' ')}"
      else
        abort "Installation of one or more plugins has failed. Aborting."
      end
  
    end
end

playbook_file = 'ansible/buildit.playbook.yml'

Vagrant.configure("2") do |config|
    config.hostmanager.enabled = true
    config.hostmanager.manage_host = true
    config.hostmanager.manage_guest = true
    config.hostmanager.ignore_private_ip = false
    config.hostmanager.include_offline = true
    
    config.vm.box = "geerlingguy/centos7"
    config.vm.hostname = "elk"
    config.vm.network "private_network", ip: elk_config.fetch(:vm_ip_address, '192.168.100.150')

    if elk_config.fetch("enable_public_network", false) 
      config.vm.network "public_network"
    end 

    config.hostmanager.aliases = %w(elk.local elk.localhost elk)

    config.vm.provider "virtualbox" do |vb|
      vb.cpus = elk_config.fetch("vm_cpus", 4)
      vb.memory = elk_config.fetch("vm_memory", 4096)
    end

     # Provision hostnmanager
     config.vm.provision :hostmanager

     # Install with ansible 
     config.vm.provision "ansible_local" do |ansible|
       ansible.playbook = playbook_file
       ansible.verbose = true
       ansible.galaxy_role_file = "ansible/requirements.yml"
     end

end