# The project has migrated over to GitLab.com

## see https://gitlab.com/bitcoinunlimited/cashnodes



# CASHNODES Crawler


Cashnodes is currently being developed to estimate the size of the Bitcoin network by finding all the reachable nodes in the network. The current methodology involves sending [getaddr](https://en.bitcoin.it/wiki/Protocol_specification#getaddr) messages recursively to find all the reachable nodes in the network, starting from a set of seed nodes. Cashodes uses Bitcoin protocol version 70015 (i.e. >= Bitcoin ABC, Bitcoin XT and BUcash). Since Bitcoin Cash network use a different set of network magic bits we are certain to avoid inclusion of Bitcoin legacy nodes in the collected data.

Currently set of [API](https://github.com/BitcoinUnlimited/cashnodes-api) and is currently providing

    GET /snapshots
    GET /snapshots/:timestamp

To deploy an instance of the crawler please have a look at the step necessary to set up a machine to run the backend code: [Provisioning Bitcoin Network Crawler](https://github.com/ayeowch/bitnodes/wiki/Provisioning-Bitcoin-Network-Crawler). The [Redis Data](https://github.com/ayeowch/bitnodes/wiki/Redis-Data) contains the list of keys and their associated values that are written by the scripts in this project.


Both aforementioned documentations are tailored for bitnodes.earn.com code base, we are going to provide a Cash version of those wiki pages as soon as things settled.

If you wish to access the data, e.g. list of network snapshots, collected using this project, see the initial set of [APIs](https://github.com/BitcoinUnlimited/cashnodes-api) we are currently developing.

## How to start the crawler

```bash
cd; wget --no-check-certificate https://github.com/BitcoinUnlimited/cashnodes/archive/master.zip
unzip master.zip
virtualenv ~/.virtualenvs/cashnodes
source ~/.virtualenvs/cashnodes/bin/activate
cd cashnodes
pip install -r requirements.txt
bash geoip/update.sh
bash start.sh
cd data/pcap/e3e1f3e8
sudo rm *.pcap
sudo tcpdump -i [INTERFACE] -w %s.[INTERFACE.pcap -v -n -G 2 -B 65536 -Z [USERNAME] 'tcp and not src host [IP_ADDRESS] and not src host [IPV6_ADDRESS]' > [INTERFACE] 2>&1 &
sudo tcpdump -i lo -w %s.lo.pcap -v -n -G 2 -B 65536 -Z [USERNAME] 'tcp and port 9050' > lo 2>&1 &
```
