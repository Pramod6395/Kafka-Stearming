# Kafka Installation

## Step 1. Install Java 11 (OpenJDK):
```bash
sudo apt update
sudo apt install openjdk-11-jdk
```

Please don’t forget to configure your operating system to use OpenJDK 11 by default. You can configure which version is the default using the following command:
```bash
sudo update-alternatives --config java

```
You can check the installation using the following command:
```bash
java -version

```
Expected command output is:
```bash
openjdk version "11.0.xx"
OpenJDK Runtime Environment (...)
OpenJDK 64-Bit Server VM (build ...)

```
## Step 2. Kafka Installation:

Kafka uses ZooKeeper so you need to first install ZooKeeper server:
```bash
sudo apt-get install zookeeper
```

Install Kafka:
```bash
wget https://archive.apache.org/dist/kafka/2.6.0/kafka_2.13-2.6.0.tgz

tar xzf kafka_2.13-2.6.0.tgz

sudo mv kafka_2.13-2.6.0 /usr/local/kafka

```

#### Setup ZooKeeper Systemd Unit file:

Create systemd unit file for Zookeeper:
```bash
sudo nano /etc/systemd/system/zookeeper.service
```
 Add below contnet:
```bash
[Unit]
Description=Apache Zookeeper server
Documentation=http://zookeeper.apache.org
Requires=network.target remote-fs.target
After=network.target remote-fs.target

[Service]
Type=simple
ExecStart=/usr/local/kafka/bin/zookeeper-server-start.sh /usr/local/kafka/config/zookeeper.properties
ExecStop=/usr/local/kafka/bin/zookeeper-server-stop.sh
Restart=on-abnormal

[Install]
WantedBy=multi-user.target

```
#### Setup Kafka Systemd Unit file
Create systemd unit file for Kafka:
```bash
sudo nano /etc/systemd/system/kafka.service
```
Add the below content. Make sure to replace “PUT_YOUR_JAVA_PATH” with your real JAVA_HOME path as per the Java installed on your system, by default like “/usr/lib/jvm/java-11-openjdk-xxx”:

```bash
[Unit]
Description=Apache Kafka Server
Documentation=http://kafka.apache.org/documentation.html
Requires=zookeeper.service

[Service]
Type=simple
Environment="JAVA_HOME=PUT_YOUR_JAVA_PATH"
ExecStart=/usr/local/kafka/bin/kafka-server-start.sh /usr/local/kafka/config/server.properties
ExecStop=/usr/local/kafka/bin/kafka-server-stop.sh

[Install]
WantedBy=multi-user.target

```

#### Start ZooKeeper and Kafka:

```bash
sudo systemctl start zookeeper

sudo systemctl start kafka

```




