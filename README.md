# CloudComputingAssignment1

## Explaining how the code works

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


## Teamwork
Xinmeng Zhang: set up VMs and configuration files

Kerou Cheng: producer.py and comsumer.py

Equal workload distribution

## Report on effort expended
We started from the async. video tutorial to set up Chameleon VMs. Then we use the scaffolding code to config the Kafka and Zookeeper settings. We experimented for several times to figure out how VM1s, VM2 and VM3 are communicated from Kafka and Zookeeper ports. We had some problems with the firewalls and solved it with ufw command. 

(###########. add comsumer drumping part. ###########. )

Finally, we correctly run the producer.py on VM1, displayed and dumped te JSON files on VM3's database. 
