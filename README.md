csv-logs-to-json
================

Logs format conversion tool (CSV to JSON).

Installation
============

    git clone https://github.com/cGuille/csv-logs-to-json.git
    cd csv-logs-to-json
    sudo npm install -g

Usage
=====
`cltj <csv formated log file>[ <output json file>]`

The output json file default name is logs.json. If the output file already exists, a copy with the '.old' extension will be created.

To get CSV formated logs on your webserver, you have to configure it. With nginx, here is how to create the log format:

    log_format csv '"$remote_addr","$remote_user","$time_local","$request","$status","$body_bytes_sent","$http_referer","$http_user_agent"';
    
Then use the format name `csv` when configuring your servers logs with the access_log command:

    access_log /path/to/access.log csv;
