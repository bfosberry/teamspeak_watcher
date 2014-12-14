teamspeak_server watcher
================

Basic watcher for a teamspeak_server

This container is to be run in parallel with a teamspeak server container, using its volumes.
Logs within the volumes are monitored for changes, and this container reacts by posting the 
values to and etcd namespace (/_$SERVER_ID/info):

* Username - the query port username
* Password - the query port password
* Admin token - the privileged key to be used on first login or to restore access

This container requires the following ENV variables to be present:

* ETCD_SERVER - the host:port of the etcd server where info should be placed
* SERVER_ID - the id/name of the server used to look up the information

To use the controller start it with the mounted volumes from the associated container

```
docker run --rm --volumes-from my_teamspeak_server -e "SERVER_ID=1234" -e "ETCD_SERVER=1.2.3.4:4001" bfosberry/teamspeak_watcher
```
 
