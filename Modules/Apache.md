# Apache configuration


## Aim
In this file we provide you an example of custom log for your apache web server.
This is not a tutorial or full web server configuration example. Only the loging part will be explained.


## Summary
1 - [Logs customization](#logs-customization)  
2 - [Sending logs directly to logstash](#sendi3ng-logs-directly-to-logstash)  
3 - [Debugging](#debugging)  
4 - [Go further](#go-further)

## Logs customization   

In your apache.conf add:
```bash
##
# Custom logging format (JSON)
##
LogFormat "{ \"@timestamp\":\"%t\", \"remote_addr\":\"%a\", \"remote_user\":\"%V\",\"body_bytes_sent\":\"%O\",\"request\":\"%U\",\"query\":\"%q\",   \"http_method\":\"%m\",    \"status\":\"%>s\",\"http_user_agent\":\"%{User-agent}i\", \"http_referrer\":\"%{Referer}i\" }" logstash_json


# TODO COmparer avec celle-ci
# LogFormat "{ \"@timestamp\": \"%{%Y-%m-%dT%H:%M:%S}t.%{msec_frac}t%{%z}t\", \"@message\": \"%m %H %U%q %s\", \"@fields\": { \"client\": \"%a\", \"duration_usec\": %D, \"status\": %s, \"request\": \"%U%q\", \"method\": \"%m\", \"protocol\": \"%H\", \"referrer\": \"%{Referer}i\", \"user-agent\": \"%{User-agent}i\" } }" logstash_json
Sign up for free
## End of custom log format
```

## Sending logs directly to logstash

Put this on every site-enabled:
CustomLog "||/usr/bin/logger -t apache -i -p local5.notice" logstash_json

And them on you syslog.conf:


## Debugging
TODO

Tha's all folks !  
Thanks for reading,
**Nodulaire**
