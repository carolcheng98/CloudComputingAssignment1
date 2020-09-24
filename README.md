# CloudComputingAssignment1

Device: xm (as VM2) and xm1 (VM3) on the Chameleon

Allow firewall, after each time the VM shuts down.

sudo ufw allow 2181    (only xm)

sudo ufw allow 9092   (both xm and xm1)

1. Login to xm using ssh
2. cd 'kafka folder in xm'
3. bin/zookeeper-server-start.sh config/zookeeper.properties
4. bin/kafka-server-start.sh config/server.properties

5. Login to xm1 using ssh
6. cd 'kafka folder in xm1'
7. bin/kafka-server-start.sh config/server.properties

8. python producer.py     (on local VM)  
9. python comsumer.py     (on xm1)
