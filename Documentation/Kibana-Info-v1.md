# Kibana

## Definition

"Kibana is an open source data visualization plugin for Elasticsearch. It provides visualization capabilities on top of the content indexed on an Elasticsearch cluster." Wikipedia.

Kibana is a visual plateforme coded in Java.

## Installation

The Installation of kibana is part of our ELK dpeloyement playbooks. Its not further bringed up here.

## Dashboard

### Keep calm and wait
Depending on the hardware and connection you may have to wait few minutes before to see anything interesting. Spam F5 will not help.
![keep kalm](Images/Kibana/Kibana-info-loading.png)

### Discover panel
![discover panel](Images/Kibana/Kibana-info-visualise.png)  

A lot of information here. You can see on the left bar:
- The selected fields for the current research ('*' mean everything).
- The fields available for search purpose

On the center:
- A bar diagram of log occurence during the last week
- The lasts raw logs logged.

You can expand the logs to see further with the arrow on the left of the timestamp:
![expaneded logs](Images/Kibana/Kibana-info-extendedLog.png)

We can see all the informations extracted by logstash from a rsyslog log (in standard log format *rfc 5424*)
