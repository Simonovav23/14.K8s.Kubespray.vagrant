# Vagrantfile

Vagrant.configure("2") do |config|
  # Используйте легковесный образ Debian
  config.vm.box = "debian/bullseye64"
  
  # Настройка сети для всех ВМ
  config.vm.network "public_network", bridge: "wlp0s20f3"
  
  # Определяем мастер-ноду
  config.vm.define "master" do |master|
    master.vm.hostname = "master"
    master.vm.provider "virtualbox" do |vb|
      vb.memory = "2048"
      vb.cpus = 2
    end
    
    # Провизионер для установки нужных пакетов
    master.vm.provision "shell", inline: <<-SHELL
      sudo apt update
      sudo apt install -y python3-pip git
      pip3 install ansible
    SHELL
  end

  # Определяем воркер-ноды
  (1..2).each do |i|
    config.vm.define "worker#{i}" do |worker|
      worker.vm.hostname = "worker#{i}"
      worker.vm.provider "virtualbox" do |vb|
        vb.memory = "2048"
        vb.cpus = 2
      end
      
      # Провизионер для установки нужных пакетов на воркер-нодах
      worker.vm.provision "shell", inline: <<-SHELL
        sudo apt update
        sudo apt install -y python3-pip git
        pip3 install ansible
      SHELL
    end
  end
end
