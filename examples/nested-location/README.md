# Nested Location Configuration

Apicast configuration uses a single location block "location /" to handle all requests. Sometimes, a custom configuration must be applied only to requests matching a URI pattern. This can be done using a configuration within a location block that matches the request URI. This example shows how to apply this customization using a location block nested within the "location /" block . 

This example shows how to configure the client_max_body_size which sets the maximum allowed size of a client request. The default configuration of Apicast (starting in 3.1.0) sets the client_max_body_size to be unlimited for all request URI. This example shows how to override that and set the client_max_body_size only for certain request URI. 

The following configuration files are used in the customization

+ http.d/core.conf . This sets the default client_max_body_size e.g. 1MB and overrides the default unlimited size.
+ apicast.d/location.d/client_config.conf - contains the location block matching the URI. The client_max_size_body is set within this block and therefore applies only to the resources matching this request URI. This location block will be nested with the "location /" . 
+ apicast.d/location.d/shared/location_directives.conf -Nginx directives to be included in a nested location block. The list includes directives used by Apicast but not inherited by a nested location block.

## Configure and Test Standalone
To apply this customization running Apicast self managed :
+ Download a 3.1.0 release of Apicast. 
+ Copy or replace the above files to the corresponding locations in the apicast v 3.1.0 tree.
+ Cange location block to match the request URI for the resource as needed.
+ Startup up Apicast 

Then try a request:
```shell  
curl http://localhost:8080 -X POST ...
```


