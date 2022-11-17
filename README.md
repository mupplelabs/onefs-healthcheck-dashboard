# onefs-healthcheck-dashboard
A grafana dashboard to visualize OneFS Healthcheck results for multiple clusters

![grafik](https://user-images.githubusercontent.com/75881070/202432427-8f9f89ab-2ffa-4f86-bb02-e9dd4114c44a.png)

1. Install Infinity Datasource Plugin (minimum version 1.2).
  Download the required version of release zip file from github and extract into your grafana plugin folder. 
  Then restart Grafana.
	
2. Install dynamic text plugin 
  https://github.com/VolkovLabs/volkovlabs-dynamictext-panel
	
3. Configure infinity plugin:
  - Name: infinity
  - Auth Type: Basic Auth
  - User: \<your API user\>
  - Password: \<your API users Password\>
  - Allowed hosts:
    - Add an entry for every fqdn of your clusters.
    - Eg. https://admin.cluster.customer.com:8080
			
  - Add reference data, a json containing a mapping between Cluster name and fqdn.   
		This is used later to navigate the dashboard. 
		Eg.:  
			{ "clusters" : [   
			{"name" : "SB2","fqdn":"10.231.153.40"},  
			{"name" : "HEXIE", "fqdn":"192.168.188.194"},  
			{"name": "gotham","fqdn":"192.168.188.93"}  
			]}  
			
4. Install the dashboard json
