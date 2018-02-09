# Nested Location Block Configuration


N.B. The following writeup applies to 3.1.0 stable release and has been tested using this release.

Apicast configuration uses a single location block "location /" to handle all requests. Sometimes, a custom configuration must be applied only to requests matching a URI pattern. A location block that matches request URI can be used for this purpose. 

The default configuration of Apicast sets the client_max_body_size to be unlimited for all request URIs. This example shows how to override that and set the client_max_body_size only for requests matching a URI pattern.
The following configuration files are used

+ http.d/core.conf . This sets the default client_max_body_size to a specific size ( e.g. 1 MB)
+ apicast.d/location.d/client_config.conf - contains the location block matching the URI. The client_max_size_body is set within this block and therefore applies only to the resources matching this request URI. This location block will be nested with the "location /" . 
+ apicast.d/location.d/shared/location_directives.conf -Nginx directives to be included in a nested location block. The list includes directives used by Apicast but not inherited by a nested location block.

## Configure and Test Standalone Apicast

+ Download a 3.1.0 release of Apicast. 
+ Copy or replace the above files to the corresponding locations in the apicast v 3.1.0 tree.
+ Change location block to match the request URI for the resource as needed.
+ Startup up Apicast 
+ Try a request: ```shell  
curl http://localhost:8080 -X POST ...
```


