### Federation Block Signing Demo

Simple demonstration of the Federation Block Signing protocol in [Elements blockchain](https://github.com/ElementsProject/elements).

This demo uses Kafka as a communication protocol between 3 signing nodes running locally, implementing a 2-of-3 Federation.

This can be easily extended for nodes running in remote locations/containers by changing the configuration accordingly.

#### Instructions

- Build Elements Daemon from [instructions](https://github.com/ElementsProject/elements/tree/elements-0.18.1.2/doc)
- Install Zookeeper and Kafka and start both services

```
$ wget http://ftp.tsukuba.wide.ad.jp/software/apache/kafka/2.3.1/kafka_2.11-2.3.1.tgz
$ tar zxf kafka_2.11-2.3.1.tgz
$ cd kafka_2.11-2.3.1
$ bin/zookeeper-server-start.sh config/zookeeper.properties &
$ bin/kafka-server-start.sh config/server.properties &
```

- Install python3 and requirements `pip3 install requirements.txt`

```
$ python3 -m venv py3
$ source py3/bin/activate
$ pip install -r requirements.txt
```

#### Demonstration

The Federation will run with a 60 second block time amd consist of 3 signing nodes by default. Nodes will connect to the kafka server running on `localhost:9092`. To change any configuration options look at: `Federation.py`, `BlockSigning.py`, `nodeX/elements.conf`.

Run the demo:

```
$ source py3/bin/activate

# You can modify ELEMENTS_PATH="/to/your/elementsd".
$ vi Federation.py

# first time(generate keys)
$ python Federation.py generate
```

```
# after creating federation_data.json
$ python Federation.py
```

The Federation could be moved to remote locations by running each node on separate locations. Localhost addresses will have to be replaced with the new remote host addresses in `elements.conf` and the `KAFKA_SERVER` parameter would have to be set to the remote address of the Kafka server. The federation script will have to be run in each remote host.
