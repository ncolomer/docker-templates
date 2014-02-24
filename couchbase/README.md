
Inspired from https://gist.github.com/dustin/6605182

edit /etc/init/docker.conf and add:
limit memlock unlimited unlimited
limit nofile 262144
service docker restart

# 3-node cluster

	docker run -d $(./scripts/ports raz) -name cb1 ncolomer/couchbase
	docker run -d $(./scripts/ports) -name cb2 ncolomer/couchbase couchbase-start $(./scripts/ipof cb1)
	docker run -d $(./scripts/ports) -name cb3 ncolomer/couchbase couchbase-start $(./scripts/ipof cb1)

# Two 2-node cluster (XDCR base)

	docker run -d $(./scripts/ports raz) -name cb11 ncolomer/couchbase
	docker run -d -name cb12 ncolomer/couchbase couchbase-start $(./scripts/ipof cb11)
	docker run -d $(./scripts/ports) -name cb21 ncolomer/couchbase
	docker run -d -name cb22 ncolomer/couchbase couchbase-start $(./scripts/ipof cb21)

using Telnet to connect to the server and using the Memcached text protocol

	$ telnet localhost
	
	# Check health
	$ stats
	
	# Set and get a key
	$ set test_key 0 0 1
	$ get test_key
	
	# Disconnect
	$ quit

open a browser http://localhost:8091/
