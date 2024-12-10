# Vagrantfile

Vagrant.configure("2") do |config|
  # Используйте легковесный образ Debian
  config.vm.box = "debian/bullseye64"
  config.vm.network "public_network", bridge: "wlp0s20f3"
  # Определяем мастер-ноду
  config.vm.define "master" do |master|
    #master.network "public_network"  # Замените на master.vm.network
    master.vm.hostname = "master"
    master.vm.provider "virtualbox" do |vb|
      vb.memory = "2048"
      vb.cpus = 2
    end
  end

  # Определяем воркер-ноды
  (1..2).each do |i|
    config.vm.define "worker#{i}" do |worker|
      #worker.network "public_network"  # Замените на worker.vm.network
      worker.vm.hostname = "worker#{i}"
      worker.vm.provider "virtualbox" do |vb|
        vb.memory = "2048"
        vb.cpus = 2
      end
    end
  end
end