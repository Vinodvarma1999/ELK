# ELK Installation and Performing ELK Hands-On Using Elasticsearch, Logstash, Kibana and beats.

## Ubuntu (t2.medium or more than 2CPU)

--> `sudo apt update` <br>
--> `sudo apt install openjdk-11-jdk -y` <br>
--> `sudo apt-get install nginx -y` <br>
--> `sudo systemctl enable nginx` <br>

## Install Elastic Search

--> `wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.2.0-amd64.deb` <br>
--> `sudo dpkg -i elasticsearch-7.2.0-amd64.deb`

## Install kibana
--> `sudo wget https://artifacts.elastic.co/downloads/kibana/kibana-7.2.0-amd64.deb` <br>
--> `sudo dpkg -i kibana-7.2.0-amd64.deb`

## Install Dependencies 
--> `sudo apt-get install -y apt-transport-https`

## Install Logstash
--> `sudo wget https://artifacts.elastic.co/downloads/logstash/logstash-7.2.0.deb` <br>
--> `sudo dpkg -i logstash-7.2.0.deb`

## Filebeat
--> `wget https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.2.0-amd64.deb` <br>
--> `sudo dpkg -i filebeat-7.2.0-amd64.deb`

## Modify elasticsearch YAML file
--> `sudo nano /etc/elasticsearch/elasticsearch.yml` <br>
#### Make below changes in this file :-
   ```sh 
    cluster.name: my-application
    node.name: node-1
    http.port: 9200
    network.host: localhost
   ```
    
--> `sudo systemctl start elasticsearch` <br>
--> `sudo systemctl status elasticsearch`

## Modify elasticsearch YAML file
--> `sudo nano /etc/kibana/kibana.yml` 
#### Make below changes in the file:-
   ```sh 
    server.port: 5601
    server.host: "localhost"
   ``` 
--> `sudo systemctl start kibana` <br>
--> `sudo systemctl status kibana` <br>
--> `sudo apt-get install -y apache2-utils` <br>
--> `sudo htpasswd -c /etc/nginx/htpasswd.users kibadmin` --(This is the Username & Password) <br>
--> `sudo nano /etc/nginx/sites-available/default`
   
 #### Paste This :-
   
            server {
                 listen 80;
 
                 server_name <PASTE_PUBLIC_IP>;
 
                 auth_basic "Restricted Access";
                 auth_basic_user_file /etc/nginx/htpasswd.users;
 
                 location / {
                        proxy_pass http://localhost:5601;
                        proxy_http_version 1.1;
                        proxy_set_header Upgrade $http_upgrade;
                        proxy_set_header Connection 'upgrade';
                        proxy_set_header Host $host;
                        proxy_cache_bypass $http_upgrade;
                 }
             }
--> `sudo systemctl restart nginx` <br>

## Paste the Public of Instances in Browser --> Provide username (kibadmin) and paassword (you provided)    
