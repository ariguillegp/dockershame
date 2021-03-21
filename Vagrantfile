image = "ubuntu/focal64"
workers = 2

Vagrant.configure("2") do |config|
    config.ssh.insert_key = false
    config.vm.provider "virtualbox" do |v|
        v.memory = 2048
        v.cpus = 2
    end

    config.vm.define "master" do |master|
        master.vm.box = image
        master.vm.network "private_network", ip: "10.18.0.11"
        master.vm.hostname = "cluster-master"
        master.vm.provision "ansible" do |ansible|
            ansible.playbook = "main.yml"
            ansible.extra_vars = {
                node: "master",
                node_ip: "10.18.0.11",
                pod_subnet: "192.168.0.0/17",
                service_subnet: "192.168.128.0/17",
                dns_domain: "cluster.local",
            }
        end
    end

    (1..workers).each do |i|
        config.vm.define "worker#{i}" do |worker|
            worker.vm.box = image
            worker.vm.network "private_network", ip: "10.18.0.#{i + 11}"
            worker.vm.hostname = "cluster-worker#{i}"
            worker.vm.provision "ansible" do |ansible|
                ansible.playbook = "main.yml"
                ansible.extra_vars = {
                    node: "worker",
                    node_ip: "10.18.0.#{i + 11}",
                }
            end
        end
    end
end
