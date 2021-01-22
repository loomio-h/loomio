# Loomio - an optimized version of Ceph

Please see http://ceph.com/ for current info.


## Abstract

Device-level interference is recognized as a major cause of the performance degradation in distributed file systems. 
Although the approaches of mitigating interference through coordination at application level, library level and 
middleware level have shown beneficial results in previous studies, we find their effectiveness is largely weakened 
since I/O requests are re-arranged by underlying object file systems. In this research study, we argue that object-level 
coordination is critical and often the key to address the interference issue, as the scheduling of object requests 
determines the devicelevel accesses and thus determines the actual I/O bandwidth and latency. This paper proposes 
an object-level coordination system, LoomIO, which uses an OBOP (One-Broadcast-OnePropagate) method and a time-limite
coordination process to deliver highly efficient coordination service. Specifically, LoomIO enables object requests to
achieve an optimized scheduling decision within a few milliseconds and largely mitigates the device-level interference issue. 
We have implemented a LoomIO prototye and integrated it into Ceph file system.

## Environment setup

### the first step

Install ceph, This step needs to be installed according to your own environment

### the second step

Install redis,Install separately on each node.
	
	cd [your installation directory]
	wget http://download.redis.io/releases/redis-5.0.8.tar.gz
	tar -zxvf redis-5.0.8.tar.gz
	cd redis-5.0.8
	sed -i 's/daemonize no/daemonize yes/' redis.conf
	sed -i 's/stop-writes-on-bgsave-error yes/stop-writes-on-bgsave-error no/' redis.conf

### the third step

Compile hiredis on each node
	
	cd [your installation directory]
	git clone https://github.com/redis/hiredis.git
	cd hiredis
	make

### the fourth step

Install hiredis,Install separately on each node.

	cd [your installation directory]/hiredis/
	sudo make install
	sudo sh -c 'echo /usr/local/lib >> /etc/ld.so.conf'
	sudo ldconfig
### the fifth step

Set the IP address to the address of the corresponding node in redis.conf

	./install-deps.sh

## test

Use FIO test


