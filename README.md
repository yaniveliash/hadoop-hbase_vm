# Hadoop + Hbase
A local deployment for development purpose on centos 7 with vagrant over virtualbox.</br>
*There is an option to download on the fly hadoop and hbase or provide your own files*

# Offline requirements
For an offline deployment you will need to provide the following 3 files and ammend the vagrantfile:
- [x] CentOS-7-x86_64-Vagrant-1801_02.VirtualBox.box
- [x] hbase-1.2.6-bin.tar.gz
- [x] hadoop-2.8.3.tar.gz

# System Resources and requirements
- [x] Vagrant 2+
- [x] Virtualbox 5+ (with support for 64bit)

> Make sure that you've enough resources to allocate, Otherwise, you will need to ammend the vagrantfile.
- [x] 4 Cores
- [x] 4G Ram

# Control
In a command line</br>
deploy: `vagrant up`</br>
destroy: `vagrant destroy`
> During `vagrant up` you will be asked to choose ethernet card for network bridge - it's usually number 1</br>
> The process won't continue unless you choose and confirm.
# Access
Once vagrant finish it thing, you will be able to see the mahcine's IP in the console output,</br>
use that IP to access your machine.</br>
</br>
HBASE WebUI is available at port : 16010</br>
Hadoop HDFS Health WebUI is available at port : 50070</br>
Hadoop cluster WebUI is available at port : 8088