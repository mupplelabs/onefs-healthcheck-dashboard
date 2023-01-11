# onefs-healthcheck-dashboard
A grafana dashboard to visualize OneFS Healthcheck results for multiple clusters

![grafik](https://user-images.githubusercontent.com/75881070/211829997-def87545-fe4b-49a8-bf40-c1b89b5f4085.png)
![grafik](https://user-images.githubusercontent.com/75881070/211830157-4c54b0f4-6a31-4c1a-9cd5-90d16dcda4f7.png)

1. Install Infinity Datasource Plugin (minimum required version 1.2).
	  - Download the required version of release zip file from github and extract into your grafana plugin folder.  
	    Then restart Grafana.
	  - Or install using the grafana plugin library.
	
2. Install dynamic text plugin via the plugin library. 
  https://github.com/VolkovLabs/volkovlabs-dynamictext-panel
  
4. equip or create a monitor user on each PowerScale Cluster with the following minimum RBAC Read Only privileges:
	  - ISI_PRIV_SYS_SUPPORT 
	  - ISI_PRIV_LOGIN_PAPI 
	  
   (Feel free to add more privilidges as required if you intend to explore more possibilities.)
   
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
```
{ "clusters" : [
	{"name" : "SB2", "fqdn" : "10.231.153.40"},
	{"name" : "HEXIE", "fqdn" : "192.168.188.194"},
	{"name" : "gotham", "fqdn" : "192.168.188.93"}
]}
```
			
5. Install the dashboard json files

# Limitations
- the inifinity datasource does not support session based authentication, hence we must utilize and enable Basic Auth on our clusters.
- the described approach uses one datasource for all clusters, hence the "monitor" users created above must have the same password on all clusters.
- on large clusters the initial load time for the HCF panels can take a couple of seconds - Patience you must have, my young padawan.
