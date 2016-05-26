# Nginx configuration


## Aim
In this file we provide you an example of custom log for your Nginx web server.
This is not a tutorial or full web server configuration example. Only the loging part will be explained.


## Summary

## Logs customization   
The simpliest way to get a custom log for every sites on your server is to define a custom log types in ```/etc/nginx/nginx.conf``` (path may change depending of the installation).
On this file, in the ```http{}``` bracket  add the following code (before the access_log and error_log prerogative):  
```
##
# Custom logging format (JSON)
##
  log_format logstash_json '{ "@timestamp": "$time_iso8601", '
                   '"@fields": { '
                   '"remote_addr": "$remote_addr", '
                   '"remote_user": "$remote_user", '
                   '"body_bytes_sent": "$body_bytes_sent", '
                   '"request_time": "$request_time", '
                   '"status": "$status", '
                   '"request": "$request", '
                   '"request_method": "$request_method", '
                   '"http_referrer": "$http_referer", '
                   '"http_user_agent": "$http_user_agent" } }';

## End of custom log format
```
As you can see a json format is used. As json is the format used by elasticsearch we gain a bit of preprocessing time by making the web server working for us. The information provided by this log are also more interesting and verbose than those by default.

Be free to send me your log_format to improve this one or only for the beauty of sharing.

## Sending logs directly to logstash

In nginx you can have multiple instance of ```access_log``` and ```error_log```. So you can send your log to multiple servers or keep logging to the local system and send them to a remote server.

To send directly your log to the logstash :
Below the custom logformat add the following lines.
```
access_log syslog:server=192.168.122.26:5014,facility=local7,tag=reverse_proxy_access,severity=info logstash_json;
error_log syslog:server=192.168.122.26:5014,tag=reverse_proxy_error debug;
```
Adapt to your needs.  
You can also add the lines on each ```sites-availables``` for custom-logs per sites.
The ```tag``` is very important, it will help you to create efficient view on Kibana.

As you can see only the access_log will use the custom log format. Nginx doesn't allow the modification of error_log.

## Debugging
In the tag name only lower alpha-numeric chars and underscore are allowed.
Compare the log provided by nginx in the local rsyslog and in your kibana to find errors.

```sudo nginx -t``` will check the configuration without restart the server. It can be helpfull.

## Go further

Nginx allow you to extract a lot of information directly in json. Most of them are hard to understand /or/ useless (because of redondancy). You can consul them [here](http://nginx.org/en/docs/ngx_core_module.html)

Tha's all folks !
Thanks for reading,
**Nodulaire**
