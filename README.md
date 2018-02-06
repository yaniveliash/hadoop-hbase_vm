# Hadoop + Hbase
A local deployment for development purpose on centos 7 with vagrant over virtualbox.</br>
*There is an option to download on the fly hadoop and hbase or provide your own files*

# Offline requirements
For an offline deployment you will need to provide the following 3 files and ammend the vagrantfile:
- [x] CentOS-7-x86_64-Vagrant-1801_02.VirtualBox.box
- [x] hbase-1.2.6-bin.tar.gz
- [x] hadoop-2.8.3.tar.gz

# System Resources
Make sure that you've enough resources to allocate
- [x] 4 Cores
- [x] 4G Ram

Otherwise, you will need to ammend the vagrantfile.

# Access
Once the machine is up and running and got a DHCP IP allocation,</br>
type `vagrant ssh` and inside the machine get your machine's IP address with `ip a`</br>
</br>
HBASE WebUI is available at port : 16010</br>
Hadoop HDFS Health WebUI is available at port : 50070</br>
Hadoop cluster WebUI is available at port : 8088