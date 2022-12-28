machines = {
  "master" => {"ip" => "100", "image" => "tknerr/baseimage-ubuntu-20.04"},
  "node01" => {"ip" => "101", "image" => "tknerr/baseimage-ubuntu-20.04"},
  "node02" => {"ip" => "102", "image" => "tknerr/baseimage-ubuntu-20.04"}
}

Vagrant.configure("2") do |config|
  machines.each do |name, conf|
    config.vm.define "#{name}" do |machine|
      machine.vm.box = "#{conf["image"]}"
      machine.vm.box_version = "1.0.0"
      machine.vm.hostname = "#{name}"
      machine.vm.network "private_network", ip: "10.10.10.#{conf["ip"]}"
      machine.vm.provider "docker" do |d|
        d.name = "#{name}"
        d.remains_running = false
      end
      
      machine.vm.provision "shell", path: "docker.sh"

      if "#{name}" == "master"
        machine.vm.provision "shell", path: "master.sh"
      else
        machine.vm.provision "shell", path: "worker.sh"
      end
    end
  end
end
