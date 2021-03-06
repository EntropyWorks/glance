Description
===========

Installs the OpenStack Image Repository/Server (codename: glance) from packages. Optionally populates the repository with some default images.

http://glance.openstack.org/

Requirements
============

Chef 0.10.0 or higher required (for Chef environment use)

Platform
--------

* Ubuntu-12.04
* Fedora-17

Cookbooks
---------

The following cookbooks are dependencies:

* database
* mysql
* keystone


Resources/Providers
===================

None


Recipes
=======

default
-------
-Includes recipes `api`, `registry`  

api
------
-Installs the glance-api server  

registry
--------
-Includes recipe `mysql:client`  
-Installs the glance-registry server  


Data Bags
=========

None


Attributes 
==========

* `glance["db"]["name"]` - Name of glance database
* `glance["db"]["user"]` - Username for glance database access
* `glance["db"]["password"]` - Password for glance database access
* `glance["api"]["ip_address"]` - IP address to use for communicating with the glance API
* `glance["api"]["bind_address"]` - IP address for the glance API to bind to
* `glance["api"]["port"]` - Port for the glance API to bind to
* `glance["api"]["adminURL"]` - Used when registering image endpoint with keystone
* `glance["api"]["internalURL"]` - Used when registering image endpoint with keystone
* `glance["api"]["publicURL"]` - Used when registering image endpoint with keystone
* `glance["registry"]["ip_address"]` - IP address to use for communicating with the glance registry
* `glance["registry"]["bind_address"]` - IP address for the glance registry to bind to
* `glance["registry"]["port"]` - IP address for the glance port to bind to
* `glance["service_tenant_name"]` - Tenant name used by glance when interacting with keystone - used in the API and registry paste.ini files
* `glance["service_user"]` - User name used by glance when interacting with keystone - used in the API and registry paste.ini files
* `glance["service_pass"]` - User password used by glance when interacting with keystone - used in the API and registry paste.ini files
* `glance["service_role"]` - User role used by glance when interacting with keystone - used in the API and registry paste.ini files
* `glance["image_upload"]` - Toggles whether to automatically upload images in the `glance["images"]` array
* `glance["images"]` - Default list of images to upload to the glance repository as part of the install
* `glance["image]["<imagename>"]` - URL location of the <imagename> image. There can be multiple instances of this line to define multiple imagess (eg natty, maverick, fedora17 etc)
--- example `glance["image]["natty"]` - "http://c250663.r63.cf1.rackcdn.com/ubuntu-11.04-server-uec-amd64-multinic.tar.gz"
* `glance["api"]["default_store"]` - Toggles the backend storage type.  Currently supported is "file" and "swift"
* `glance["api"]["swift"]["store_container"] - Set the container used by glance to store images and snapshots.  Defaults to "glance"
* `glance["api"]["swift"]["store_large_object_size"] - Set the size at which glance starts to chunnk files.  Defaults to "200" MB
* `glance["api"]["swift"]["store_large_object_chunk_size"] - Set the chunk size for glance.  Defaults to "200" MB


Templates
=========

* `glance-api-paste.ini.erb` - Paste config for glance-api middleware
* `glance-api.conf.erb` - Config file for glance-api server
* `glance-registry-paste.ini.erb` - Paste config for glance-registry middleware
* `glance-registry.conf.erb` - Config file for glance-registry server
* `glance-scrubber.conf.erb` - Config file for glance image scrubber service
* `policy.json.erb` - Configuration of ACLs for glance API server


License and Author
==================

Author:: Justin Shepherd (<justin.shepherd@rackspace.com>)  
Author:: Jason Cannavale (<jason.cannavale@rackspace.com>)  
Author:: Ron Pedde (<ron.pedde@rackspace.com>)  
Author:: Joseph Breu (<joseph.breu@rackspace.com>)  
Author:: William Kelly (<william.kelly@rackspace.com>)  
Author:: Darren Birkett (<darren.birkett@rackspace.co.uk>)  
Author:: Evan Callicoat (<evan.callicoat@rackspace.com>)  

Copyright 2012, Rackspace US, Inc.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
