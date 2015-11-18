solr
====

How to install
--------------
```bash
apt-get install openjdk-8-jre
wget http://apache.mirror1.spango.com/lucene/solr/5.3.1/solr-5.3.1.tgz
tar xzf solr-5.3.1.tgz solr-5.3.1/bin/install_solr_service.sh --strip-components=2
./install_solr_service.sh solr-5.3.1.tgz
```

How to setup first clone
------------------------
```bash
su - solr -c "/opt/solr/bin/solr create -c gettingstarted -n data_driven_schema_configs"
```

How to restart
--------------
```bash
/opt/solr/bin/solr restart
```
