# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "precise64"
  config.vm.box_url = "https://atlas.hashicorp.com/hashicorp/boxes/precise64/versions/1.1.0/providers/virtualbox.box"

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "tests/test.yml"
    ENV['ANSIBLE_ROLES_PATH'] = '..'
    ansible.raw_arguments = [ '--sudo' ]
    ansible.verbose = "v"
  end
end
