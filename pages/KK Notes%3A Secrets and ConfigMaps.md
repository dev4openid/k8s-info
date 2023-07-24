- # Notes: Secrets and ConfigMaps
  title:: KK Notes: Secrets and ConfigMaps
- [[Secrets]] and [[ConfigMaps]]
- config data:
	- passing arguments
	- config files
	- env variables
- configMap is limited to 1 Mb
- elements of configMap (==env variables==) are not updated in the pods when the updated configMap is applied - the pods need to be deleted and recreated (be careful)