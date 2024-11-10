Vagrant.configure("2") do |config|
  # Usamos una máquina base de Ubuntu 18.04
  config.vm.box = "ubuntu/bionic64"

  # Redirección de puertos para que el puerto 80 de la VM esté disponible en el puerto 8080 de la máquina host
  config.vm.network "forwarded_port", guest: 80, host: 8080

  # Configuramos la memoria RAM y los CPUs de la máquina virtual
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "512"  # 512MB de RAM
    vb.cpus = 1        # 1 CPU
  end

  # Instalamos Apache en la máquina virtual
  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update -y
    sudo apt-get install apache2 -y
    sudo systemctl enable apache2
    sudo systemctl start apache2
    echo "Hola Mundo desde Apache en Vagrant!" | sudo tee /var/www/html/index.html
  SHELL

  # Compartimos la carpeta local "paginas_web" con el directorio de Apache
  config.vm.synced_folder "paginas_web", "/var/www/html"
end
