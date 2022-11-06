Vagrant.configure("2") do |config|
    config.vm.box = "generic/arch"
    config.vm.synced_folder ".", "/home/vagrant/dev"
    config.vm.network "forwarded_port", guest: 80, host: 8080
    config.vm.provision "shell", reboot: true, inline: <<-SHELL
        sudo pacman -Syu --noconfirm docker docker-compose 
        sudo usermod -aG docker vagrant
        sudo systemctl enable docker.service
    SHELL
    config.vm.provision "shell", run: "always", inline: <<-SHELL
        docker-compose -f /home/vagrant/dev/docker-compose.yml up -d
    SHELL
end
