# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
    config.vm.box = "centos/7"
    #config.vm.box_url = "file:///c:/Users/Yaniv/Downloads/CentOS-7-x86_64-Vagrant-1801_02.VirtualBox.box"
    config.vm.network "public_network"
    config.vm.provider "virtualbox" do |vb|
    vb.name = "hadoop_hbase"
    vb.customize [
        'modifyvm', :id,
        '--natdnshostresolver1', 'on',
        '--memory', '4096',
        '--cpus', '4'
      ]
end
# Change the below lines if you provide a pre-downloaded tars of hadoop and hbase
#config.vm.provision "file", source: "./hbase-1.2.6-bin.tar.gz", destination: "/home/vagrant/hbase-1.2.6-bin.tar.gz"
#config.vm.provision "file", source: "./hadoop-2.8.3.tar.gz", destination: "/home/vagrant/hadoop-2.8.3.tar.gz"
config.vm.provision "file", source: "./core-site.xml", destination: "/home/vagrant/core-site.xml"
config.vm.provision "file", source: "./hdfs-site.xml", destination: "/home/vagrant/hdfs-site.xml"
config.vm.provision "file", source: "./mapred-site.xml", destination: "/home/vagrant/mapred-site.xml"
config.vm.provision "file", source: "./yarn-site.xml", destination: "/home/vagrant/yarn-site.xml"
config.vm.provision "file", source: "./hbase-site.xml", destination: "/home/vagrant/hbase-site.xml"
config.vm.provision "shell", inline: <<-SHELL
    sudo useradd hadoop
    sudo passwd -d hadoop
    sudo usermod -aG wheel hadoop
    #
    # Remove these 2 lines if you provide hadoop and hbase pre-downloaded tars
    wget http://apache.spd.co.il/hbase/stable/hbase-1.2.6-bin.tar.gz 
    wget http://apache.mivzakim.net/hadoop/common/hadoop-2.8.3/hadoop-2.8.3.tar.gz
    #
    tar -zxf /home/vagrant/hadoop-2.8.3.tar.gz
    sudo mv /home/vagrant/hadoop-2.8.3 /usr/local/hadoop
    sudo mv /home/vagrant/core-site.xml /usr/local/hadoop/etc/hadoop
    sudo mv /home/vagrant/hdfs-site.xml /usr/local/hadoop/etc/hadoop
    sudo mv /home/vagrant/mapred-site.xml /usr/local/hadoop/etc/hadoop
    sudo mv /home/vagrant/yarn-site.xml /usr/local/hadoop/etc/hadoop
    #
    tar -zxf /home/vagrant/hbase-1.2.6-bin.tar.gz
    sudo mv /home/vagrant/hbase-1.2.6 /usr/local/Hbase
    sudo mv /home/vagrant/hbase-site.xml /usr/local/Hbase/conf
    #
    sudo touch /etc/profile.d/global-env.sh
    sudo chmod 777 /etc/profile.d/global-env.sh
    sudo echo "export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.161-0.b14.el7_4.x86_64/jre" >> /etc/profile.d/global-env.sh
    sudo echo "export HADOOP_HOME=/usr/local/hadoop" >> /etc/profile.d/global-env.sh
    sudo echo "export HBASE_HOME=/usr/local/Hbase" >> /etc/profile.d/global-env.sh
    sudo echo 'export PATH=$PATH:$HADOOP_HOME/sbin:$HADOOP_HOME/bin:$HBASE_HOME/bin' >> /etc/profile.d/global-env.sh
    #
    sudo yum update -y
    sudo yum install wget java-1.8.0-openjdk -y
    #
    sudo su
    eval `ssh-agent`
    ssh-keygen -f /root/.ssh/id_rsa -t rsa -N ''
    touch /root/.ssh/authorized_keys
    cat /root/.ssh/id_rsa.pub > /root/.ssh/authorized_keys
    chmod 0600 /root/.ssh/authorized_keys
    ssh-add /root/.ssh/id_rsa
    ssh-keyscan localhost >> /root/.ssh/known_hosts
    export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.161-0.b14.el7_4.x86_64/jre
    /usr/local/hadoop/bin/hdfs namenode -format
    echo "yes" | /usr/local/hadoop/sbin/start-dfs.sh
    /usr/local/hadoop/sbin/start-yarn.sh
    /usr/local/Hbase/bin/start-hbase.sh
    SHELL
end