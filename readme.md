# SimpleDAV

Simple WebDAV server via docker container that isolates server enviroment and
allows external folders to be managed through bind exposition to docker /dav/
folder mount.

## Running

* `bin/docker build`
* edit configuration in `etc/conf` as needed
* `bin/pwd $scope $username` where scope defines distinct nginx configurations
and username is the name used when connecting to webDAV server.
* `bin/docker run`


## Configuration Files

### etc/conf

* `userid=1000` userid to match system user, this way has no permission errors
* `mount=EXTERNAL_PATH:INTERNAL_PATH` used to make dav written files be acessed
system wide. Can hava multiple lines with `mount=` configurations.


### etc/nginx/nginx.conf
### etc/nginx/sites-enabled/SCOPE.conf

Nginx configuration replicated to server


### etc/nginx/pwd/SCOPE.list

Passwords generated for SCOPE using bin/pwd


## Scopes

It is nothing more that some type of code organization:
* Each nginx/sites-enabled/SCOPE.list file should have only one webdav server.
* Each webdav server (SCOPE) should have one root directory
* Each root directory of each SCOPE should have one `mount=` directive on
/etc/conf file
* And each SCOPE should have one etc/nginx/pwd/SCOPE.list file generated using
bin/pwd file

That's all.
