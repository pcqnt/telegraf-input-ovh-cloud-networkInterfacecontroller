# telegraf-input-ovhcloud-networkInterfacecontroller
Python script to parse the output of [OVHcloud baremetal server network usage](https://api.ovh.com/console/#/dedicated/server/%7BserviceName%7D/networkInterfaceController~GET) into the [InfluxDB line protocol](https://docs.influxdata.com/influxdb/latest/reference/syntax/line-protocol/). Intended to be run via Telegraf's [exec](https://github.com/influxdata/telegraf/tree/master/plugins/inputs/exec) input plugin.

## Requirements
OVHcloud Python module (pip install ovh). Other requirements are listed in requirements.txt.

## Install
Configure Telegraf as shown below. Make sure to have the following environnement variables set:
```
OVH_APP_KEY
OVH_APP_SECRET
OVH_CONSUMER_KEY
```
These can be generated on [OVHcloud's portal](https://help.ovhcloud.com/csm/en-gb-api-getting-started-ovhcloud-api?id=kb_article_view&sysparm_article=KB0042784#advanced-usage-pair-ovhcloud-apis-with-an-application).
If needed you can build a docker container with the provided Dockerfile.

## Configuration

`/etc/telegraf/telegraf.conf`
```
[[inputs.exec]]
   commands = ["python3 /usr/src/app/input-ovh-networkInterfaceController.py"]
   data_format = "influx"
   interval = "1h"
   timeout = "600s"

```

## Sample output for one server
```
$ python3 ./input-ovh-networkInterfaceController.py 
ovh-baremetal-network,server=ns1234567.ip-1-2-3.eu,linkType=public,mac=0c:c4:7b:c8:d1:bb traffic_upload=194122.666 1682322629000000000
ovh-baremetal-network,server=ns1234567.ip-1-2-3.eu,linkType=public,mac=0c:c4:7b:c8:d1:bb traffic_upload=190864.893 1682323231000000000
ovh-baremetal-network,server=ns1234567.ip-1-2-3.eu,linkType=public,mac=0c:c4:7b:c8:d1:bb traffic_upload=192740.64 1682323826000000000
ovh-baremetal-network,server=ns1234567.ip-1-2-3.eu,linkType=public,mac=0c:c4:7b:c8:d1:bb traffic_upload=195781.333 1682324428000000000
ovh-baremetal-network,server=ns1234567.ip-1-2-3.eu,linkType=public,mac=0c:c4:7b:c8:d1:bb traffic_upload=192994.688 1682325030000000000
ovh-baremetal-network,server=ns1234567.ip-1-2-3.eu,linkType=public,mac=0c:c4:7b:c8:d1:bb traffic_download=197817.28 1682322625000000000
ovh-baremetal-network,server=ns1234567.ip-1-2-3.eu,linkType=public,mac=0c:c4:7b:c8:d1:bb traffic_download=194467.413 1682323227000000000
ovh-baremetal-network,server=ns1234567.ip-1-2-3.eu,linkType=public,mac=0c:c4:7b:c8:d1:bb traffic_download=196453.853 1682323829000000000
ovh-baremetal-network,server=ns1234567.ip-1-2-3.eu,linkType=public,mac=0c:c4:7b:c8:d1:bb traffic_download=199331.026 1682324431000000000
ovh-baremetal-network,server=ns1234567.ip-1-2-3.eu,linkType=public,mac=0c:c4:7b:c8:d1:bb traffic_download=196615.334 1682325026000000000
ovh-baremetal-network,server=ns1234567.ip-1-2-3.eu,linkType=public,mac=0c:c4:7b:c8:d1:bb errors_upload=0.0 1682322625000000000
ovh-baremetal-network,server=ns1234567.ip-1-2-3.eu,linkType=public,mac=0c:c4:7b:c8:d1:bb errors_upload=0.0 1682323227000000000
ovh-baremetal-network,server=ns1234567.ip-1-2-3.eu,linkType=public,mac=0c:c4:7b:c8:d1:bb errors_upload=0.0 1682323829000000000
ovh-baremetal-network,server=ns1234567.ip-1-2-3.eu,linkType=public,mac=0c:c4:7b:c8:d1:bb errors_upload=0.0 1682324431000000000
ovh-baremetal-network,server=ns1234567.ip-1-2-3.eu,linkType=public,mac=0c:c4:7b:c8:d1:bb errors_upload=0.0 1682325026000000000
ovh-baremetal-network,server=ns1234567.ip-1-2-3.eu,linkType=public,mac=0c:c4:7b:c8:d1:bb errors_download=0.0 1682322625000000000
ovh-baremetal-network,server=ns1234567.ip-1-2-3.eu,linkType=public,mac=0c:c4:7b:c8:d1:bb errors_download=0.0 1682323227000000000
ovh-baremetal-network,server=ns1234567.ip-1-2-3.eu,linkType=public,mac=0c:c4:7b:c8:d1:bb errors_download=0.0 1682323829000000000
ovh-baremetal-network,server=ns1234567.ip-1-2-3.eu,linkType=public,mac=0c:c4:7b:c8:d1:bb errors_download=0.0 1682324431000000000
ovh-baremetal-network,server=ns1234567.ip-1-2-3.eu,linkType=public,mac=0c:c4:7b:c8:d1:bb errors_download=0.0 1682325026000000000
ovh-baremetal-network,server=ns1234567.ip-1-2-3.eu,linkType=public,mac=0c:c4:7b:c8:d1:bb packets_upload=255.585 1682322627000000000
ovh-baremetal-network,server=ns1234567.ip-1-2-3.eu,linkType=public,mac=0c:c4:7b:c8:d1:bb packets_upload=251.363 1682323229000000000
ovh-baremetal-network,server=ns1234567.ip-1-2-3.eu,linkType=public,mac=0c:c4:7b:c8:d1:bb packets_upload=253.821 1682323831000000000
ovh-baremetal-network,server=ns1234567.ip-1-2-3.eu,linkType=public,mac=0c:c4:7b:c8:d1:bb packets_upload=257.791 1682324426000000000
ovh-baremetal-network,server=ns1234567.ip-1-2-3.eu,linkType=public,mac=0c:c4:7b:c8:d1:bb packets_upload=254.051 1682325028000000000
ovh-baremetal-network,server=ns1234567.ip-1-2-3.eu,linkType=public,mac=0c:c4:7b:c8:d1:bb packets_download=256.518 1682322630000000000
ovh-baremetal-network,server=ns1234567.ip-1-2-3.eu,linkType=public,mac=0c:c4:7b:c8:d1:bb packets_download=252.248 1682323225000000000
ovh-baremetal-network,server=ns1234567.ip-1-2-3.eu,linkType=public,mac=0c:c4:7b:c8:d1:bb packets_download=254.851 1682323827000000000
ovh-baremetal-network,server=ns1234567.ip-1-2-3.eu,linkType=public,mac=0c:c4:7b:c8:d1:bb packets_download=258.503 1682324429000000000
ovh-baremetal-network,server=ns1234567.ip-1-2-3.eu,linkType=public,mac=0c:c4:7b:c8:d1:bb packets_download=254.966 1682325031000000000

```
## Dashboard
A sample Grafana dashboard is present in the grafana-dashboard folder. It will query an Influxdbv2 database for results and graph result as below (with a dropdown menu of all available servers in your OVHcloud account) :  
![alt screencapture](https://raw.githubusercontent.com/pcqnt/telegraf-input-ovhcloud-networkInterfacecontroller/main/grafana-dashboard/capture_grafana.png)

Influxdbv2 output configuration in telegraf : 
```
[[outputs.influxdb_v2]]
   urls = ["http://influxdb:8086"]
   token = "redacted"
   organization = "ovh"
   bucket = "network-poll"
```
