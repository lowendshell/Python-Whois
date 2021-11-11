# Python Whois Website

A simple whois script written in Python with the support of Flask.

I've tried `whois`, `python-whois` module etc. from pypi, but no one satisfy my requirements. 
And I found the whois tool from Ubuntu is very useful. So I get 
whois information from Ubuntu shell. 

**Only support Ubuntu OS now.**

**Support all tlds.**

Visit http://www.pywhois.com for a demo.

## Deployment

Requirements:

 - Ubuntu 20.04 LTS
 - Python 3.8

Install dependency:

 - apt install whois
 - pip3 install flask

Install a web server. You can choose apache, nginx or whatever you like.

Configura the web server.

For more deployment options, see:https://flask.palletsprojects.com/en/2.0.x/deploying/

Or you can just run this script with `nohup` and redirect the domain name to `localhost:5001`

    nohup python3 -u pywhois.py > out.log 2>&1 &

Here is my example conf file for nginx server:

    location /
    {
        proxy_pass       http://localhost:5001;
        proxy_set_header Host localhost;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header REMOTE-HOST $remote_addr;
        add_header       X-Cache $upstream_cache_status;
        add_header       Cache-Control no-cache;
    }

Here is my example conf file for apache server:

    <VirtualHost *:80>
    ServerName YOURDOMAIN.NAME
    ServerAlias YOURDOMAIN.NAME www.YOURDOMAIN.NAME
    ProxyPass / http://localhost:5001/
    ProxyPassReverse / http://localhost:5001/
    ErrorLog  /data/wwwlog/YOURDOMAIN.NAME/error.log
    TransferLog  /data/wwwlog/YOURDOMAIN.NAME/access.log
    </VirtualHost>

## Usage

This tool support two usages:
 - Search whois information directly through home page
 - Get whois information with '/whois/your_domain'

 ## TODO

 - Whois information extract.
 - Rewrite the templates.

 ## Contact

 Email: mail@ztang.com

 ## Changelog
 
[0.5] - 2021-11-11
 - Fix bugs with Python3.

[0.4] - 2019-07-30
 - Fix bugs.

[0.3] - 2017-05-12
 - Rebuild with Python.
 - Change the whois lookup method.
 - Support all tlds.

[0.2] - 2015-12-10
 - Rebuild the page with Bootstrap.
 - Fix some problems with domain lookup.
 - Add some common tlds.

[0.1] - 2014-07-19
 - Whois Lookup online.
