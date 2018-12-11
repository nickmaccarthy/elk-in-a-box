# ELK In A Box

This is an ELK (Elasticsearch Logstash and Kibana) stack that is defined, built and deployed to run on your local machine within Vagrant.  This is a personal project I use to test out [Tattle](http://tattle.io) as well as various other configurations for the ELK stack.

In most of my ELK deployments I test to use RabbiqMQ as a log buffer before data is sent to Elasticsearch.  This system tries to emulate that here as well.

## Software
* OS: CentOS 7 
* Logstash 6.x
* Elasticsearch 6.x
* Filebeat 6.x
* RabbitMQ 3.6
* Kibana 5.6
* Grafana 5+

## Requirements
* Vagrant
* Virtualbox
* Ansible
* Administrative rights on you local machine

## Ports and Services
Default VM IP is `192.168.100.150`
Note: `Vagrant Host Manager` creates the alias `elk.local` on your local machines `/etc/hosts` file.  So you can access this system with `elk.local:<port>` in your browser, or by clikcing the links below.  
* Elasticsearch `tcp 9200` - [http://elk.local:9200](http://elk.local:9200) - no login
* Kibana `tcp 5601`- [http://elk.local:5601](http://elk.local:5601) - no login 
* Grafana `tcp 3000` - [http://elk.local:3000](http://elk.local:3000) - login - admin/admin 
* RabbitMQ `tcp 15672` - [http://elk.local:15672](http://elk.local:15672) - login - admin/admin

## Usage
1. Clone this repo to a directory of your choice, and then navigate to that directroy when you get there

* To start the system simply run
    * `vagrant up`
    * Note: you will need to provide your local `admin` password during the first run of `vagrant up` since the `Vagrant Host Manager` needs to modify your local `/etc/hosts` file
