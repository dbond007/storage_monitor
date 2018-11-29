# Vmax/VNX Monitor Toolkit (Ruby)
Vmax/VNX Monitoring using InfluxDB and Grafana

InfluxDB Time-Series https://www.influxdata.com/

InfluxDB GEM https://github.com/influxdata/influxdb-ruby
```
gem install influxdb
```
Grafana for visualization: https://grafana.com/

## References
https://github.com/stevenctong/vmax_monitoring - Used as reference to develop the code in Ruby 
https://github.com/ciarams87/PyU4V - I got many problems trying to install some python libraries on my Linux machine, so I decided to recode some functions from PyU4V in Ruby.

## RUVNX.rb
  Script that runs the commands via navseccli on VNX array's to get performance data

## vnx__monitoring.rb
  File that make the requests, parse data and put in InfluxDB
  
  You must initialize a new instance of the VnxGetter class and set the follow attributes:
  ```
  collect_vnx = VnxGetter.new
  collect_vnx.username =
  collect_vnx.password =
  collect_vnx.scope = 0
  collect_vnx.ip = ARGV[0]
  collect_vnx.nav_path = '/opt/Navisphere/bin' #Path of Navseccli in your system
  ```

  Usage:
  ```
  ruby vnx__monitoring.rb <vnxip>
  ```



## U4V.rb 
  Dell/EMC Have developed a module called PyU4V as a solution to make requests to the Unisphere API, unfortunattely Ruby don't have a gem that can realize the same, so I recoded some functions from PyU4V in Ruby
  
## unisphere_rest.rb (Unisphere API Requester)
  Used to request the Unisphere Api. 
  
  Before start, you need to configure the header section that authenticate with Unisphere.
  ```
    @header = {
    'Authorization' => '%ENCODED AUTHORIZATION%',
    'Content-Type' => 'application/json',
    'Accept' => 'application/json'
  }
```
  Replace '%ENCODED AUTHORIZATION%' with your username/password encoded in Base64.
  
## influxdb_connection.rb (InfluxDB Configuration)
Replace the line above with  your DB name (collect), username (admin) and password (admin).
```
  influxdb = InfluxDB::Client.new 'collect', username: 'admin', password: 'admin', precision: 's'
```

## vmax_monitoring.rb
Here is the code of all the functions that collect the metrics to generate the dashboard.
The usage of the script is:
```
ruby vmax_monitoring.rb <hostname or hostip>
```

## dashboard.json
Grafana dashboard exported in json format.


## Grafana Dashboard Screenshot 
![alt text](https://raw.githubusercontent.com/FakeCast/vmax_monitor/master/dashboard.PNG)
![alt text](https://raw.githubusercontent.com/FakeCast/vmax_monitor/master/storagegroup.PNG)
![alt text](https://raw.githubusercontent.com/FakeCast/vmax_monitor/master/hostmetric.PNG)
![alt text](https://raw.githubusercontent.com/FakeCast/vmax_monitor/master/end.png)
