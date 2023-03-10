# ---------< Loading and Analyzing .CSV data on Kibana >-----------

## Now let's imagine are we have .csv data and we need to load it Let's see how that data will be loaded.

--> `cd /home/ubuntu`

--> `curl -O https://raw.githubusercontent.com/PacktPublishing/Kibana-7-Quick-Start-Guide/master/Chapter02/crimes_2001.csv`

--> `cd /etc/logstash/conf.d/`

--> `sudo nano crimes.conf`

``` sh
			input {
				file {
					path => "/home/ubuntu/crimes_2001.csv"
					start_position => beginning
				}
			}
			filter {
				csv {
					columns => [
							"ID",
							"Case NUmber",
							"Date",
							"Block",
							"IUCR",
							"Primary Type",
							"Description",
							"location Description",
							"Arrest",
							"Domestic",
							"Beat",
							"District",
							"Ward",
							"Community Area",
							"FBI Code",
							"X Coordinate",
							"y Coordinate",
							"Year",
							"Updated On",
							"latitude",
							"longitude",
							"location"
					]
					separator => ","
					}
			}
			output {
				elasticsearch {
					action => "index"
					hosts => ["localhost"]
					index => "crimes"
				}
			}
```
--> `change 'path' to '/home/ubuntu/crimes_2001.csv'` <br>

--> `change output -> elasticsearch -> hosts to ["localhost:9200"]` <br>

--> `sudo systemctl restart logstash` <br>

### Go to kibana -> management -> kibana -> index patterns -> create index pattern -> wait for data to load up -> 'crimes*' -> next step -> @timestamp -> create index pattern 

### Go to 'Discover' ->	'crimes*'

### If you wish you can save the filter currently in use by clicking on 'save' above the search bar\

### If you want to use more than oone filter you can either use the 'add filter' or type 'keyword and keyword' in the search bar eg. 'FBI code.keyword: 14 and Date.keyword: "05/01/2015" 12:00:00 PM"'

### To save this query just hit save and it will save the filter that is your complex query making it easy to acces again

### click on 'open' -> you can search for your filter that was saved
