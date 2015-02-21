Vagrant.configure('2') do |config|
  config.vm.box      = 'ubuntu/trusty32'
  config.vm.box_url  = 'ubuntu/trusty32.json'
  config.vm.hostname = 'sugar-dev-box'

  config.vm.network :forwarded_port, guest: 3000, host: 3000

  config.vm.provision :shell, path: 'bootstrap.sh', keep_color: true
end
