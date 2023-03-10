# ---< Configuring Real Time Web logs to inject into Elasticsearch >---

## Be in a home directory i.e /home/ubuntu

--> `sudo filebeat modules list`

--> `sudo filebeat modules enable system`

--> `sudo filebeat modules enable nginx`

--> `sudo filebeat modules list`

--> `cd /etc/filebeat/modules.d`

--> `sudo nano system.yml`

### write below syslog: -> `enabled : var.paths: ["/var/log/syslog*"]`
			 	
### write below auth: -> `enabled : var.paths: ["/var/log/auth.log*"]`

--> `sudo nano nginx.yml`
			
### write below access: -> `enabled : var.paths: ["/var/log/nginx/access.log*"]`
			 	
(we will also give the path for auth log, it will tell us who all have logged in or logged out)

### write below error: -> `enabled : var.paths: ["/var/log/nginx/error.log*"]`

--> `sudo systemctl start filebeat `

# ---------< Visualisation for the static data (logstash, crimes) >---------


### ---------< Line graph Visualisation >---------


#### • Go to browser -> visualize (below discover) -> create new visualization -> 'area' -> 'petclinic-prd-1*'(data to be loaded)

#### • It will open up a dashboard with a graph where you can chose what kind of way you wish to represent your data.

#### • Under 'Y-axis' -> aggregation -> 'count'	-> custom label -> 'HTTP Requests' -> click on 'add metrics'

#### • Under 'X-axis' -> aggregation -> 'count' -> field -> 'response.keyword' -> order by -> 'metric: HTTP Requests'

#### • Go ahead and click the 'play logo' below the data name 

#### • Under metrics & axes you can change the type of chart type, mode

#### • Try changing the field to 'geoip.country_name:keyword' in the X-axis

#### • Try changing the field to 'geoip.timezone:keyword' in the X-axis

#### • Once you have created a visualization you can go ahead and save it and the button will be on top left

#### • Save it as '[apache] Total requests based on TImeZone'

#### • So if you go back and need to come and check the visualizations you had created before you can check it under visualize as it wuold now be saved

# ---------< Heat Map Visualisation >---------

#### • Now let's try this again with another type of chart type - 'Heat map'

#### • Go to browser -> visualize (below discover) -> create new visualization -> 'heatmap' -> 'crimes*'(data to be loaded)

`Aggregation -> 'count'`

`Custom label -> 'FBI code'`

`Under x-axis -> aggregation -> 'Terms' -> field -> 'FBi code.keyword' -> order by -> 'metric: FBI code'`

#### • Go ahead and click the 'play logo' below the data name 

#### • We can also see how many hits each section of the heat map has.

# ---------< Coordinate map Visualisation >---------

#### • Go to browser -> visualize (below discover) -> create new visualization -> 'heatmap' -> 'petclinic-prd-1*'

```sh
Under Buckets

'Geo Coordinates'

Aggregation -> 'geohash'-> field -> 'geoip.location'

Under options

You can change the color

So you can now see where your http requests are coming from and accordingly plan 

Now go ahead and save this visualizations as [apache] geo IP
```

# ---------< creating dashboard >---------

#### • Go to dashboard (below discover)

#### • Click on 'Create new dashboard'

#### • Click on 'add' -> [apache] geo IP & [apache] Total requests based on TimeZone

#### • You can also resize the visualisation windows acc to your need

#### • Then you can save it as 'apache dashboard'

# ---------< Visualisation for the static data (nginx, system) >---------

#### Go to home -> Mangement -> kibana -> index patterns (under kibana) -> create index pattern
	
#### Enter:- `'filebeat*' -> '@timestamp'` 	
	
--> In terminal Run:- `sudo filebeat setup -e`

#### Now let's go to ELK -> kibana -> visualisations 

#### In the search bar we will type 'nginx'  and we will get some visualizations relating to it.

#### Click on 'dashboards [filebeat Nginx] ECS'

#### Go to dashboard -> search 'nginx'

#### Click on '[filebeat nginx] Overview ECS'

#### You can now see a dashboard with multitude of details - we can see if it is doing it real time or not by hitting the webserver from a different browser

#### Just refresh and you will see all the new data

#### Then just explore the dashboard and try to understaand what all stuff you see

#### There is a machine learning feature too, but it's a paid feature

#### There is also a automated report generation option, alos paid feature

#### There is a notification system which is also a paid feature
