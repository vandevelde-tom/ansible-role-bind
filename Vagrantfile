# vi: set ft=ruby

require 'rbconfig'

ROLE_NAME = 'bind'
BASE_NAME = 'test' + ROLE_NAME
hosts = [
  { name: 'master', ip: '192.168.56.53' },
  { name: 'slave' , ip: '192.168.56.54' }
]
VAGRANTFILE_API_VERSION = '2'

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = 'bento/centos-7.4'

  hosts.each do |host|
    host_name = BASE_NAME + host[:name]

    config.vm.define host_name do |node|
      node.vm.hostname = host_name
      node.vm.network 'private_network', ip: host[:ip]
      node.vm.provision 'ansible' do |ansible|
        ansible.playbook = 'test.yml'         # Elaborate test that shows all features
        # ansible.playbook = 'test-bare.yml'  # Minimal test case
      end
    end
  end
end

