# CloudComputingAssignment1
TEAM3: Xinmeng Zhang, Kerou (Carol) Cheng

## Explaining how the code works

Device: xm (as VM2) and xm1 (VM3) on Chameleon

### Allow firewall, after each time the VMs shuts down.
`sudo ufw allow 2181`    (only xm)
`sudo ufw allow 9092`   (both xm and xm1)

### Starting Zookeeper and Kafka servers on xm (VM2)
1. Login to xm using ssh
2. cd 'kafka folder in xm'
3. Start zookeeper server: `bin/zookeeper-server-start.sh config/zookeeper.properties`
4. Start Kafka server: `bin/kafka-server-start.sh config/server.properties`
5. Create Topic on server: `bin/kafka-topics.sh --create --topic utilizations --bootstrap-server <addr>:9092`

### Starting Kafka server on xm1 (VM3)
1. Login to xm1 using ssh
2. cd 'kafka folder in xm1'
3. Start Kafka server: `bin/kafka-server-start.sh config/server.properties`

### Running producer and consumer scripts
1. clone this repository on both local VMs and xm1 (VM3)
2. Run producer script on local VM: `python3 producer.py` (cd into correct directory)
2. Run consumer script on xm1 (VM3): `python3 consumer.py` (cd into correct directory)
Note: consumer is set to receive two topics: `topic1` and `topic2`. 

### Checking couchDB status
We first created a couchDB database called test-db1 on VM3. In `consumer.py`, a Kafka consumer receives messages and store the messages in this database after decoding them. We can use curl to check the status of database and read contents.
* To check the existing database, run:
```bash
curl -X GET http://admin:123456@127.0.0.1:5984/_all_dbs
```
* To read contents from test-db1, run:
```bash
curl -X GET http://admin:123456@127.0.0.1:5984/test-db1/_all_docs
```


## Teamwork
Xinmeng Zhang: set up VMs and configuration files

Kerou (Carol) Cheng: `producer.py` and `consumer.py` | couchDB set up

Equal workload distribution

## Report on effort expended
We started from the async. video tutorial to set up Chameleon VMs. Then we used the scaffolding code to config the Kafka and Zookeeper settings. We experimented for several times to figure out how VM1s, VM2 and VM3 are communicated from Kafka and Zookeeper ports. We had some problems with the firewalls and solved it with ufw command. 

As for the producer and consumer codes for Kafka, we started off by going through several online tutorials to understand the basic concepts of producers, consumers, brokers, topics and partitions. Then we read the documentations of [couchDB](https://docs.couchdb.org/) and [pycouchDB](https://couchdb-python.readthedocs.io/en/latest/), and set up the database on VM3. We experiemented several times by altering parts of consumer and producer codes before we finally got the codes working. 

Finally, we correctly ran the producer.py on VM1, displayed and dumped the JSON files on VM3's database. 
