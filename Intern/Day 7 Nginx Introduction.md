
### Nginx

Nginx is a web server built on 2004 AD .It can act as a reverse proxy, load balancer, mail proxy and HTTP cache. It main features include :
1. Load Balancing :- It helps in load balancing by distributing network traffic equally across a pool of servers that support an application.
2. Caching :- Nginx caching features helps for overall delay when browsing the Web.
3. Compression :- Nginx also helps in compression of traffic data internet.
4. Security :- Nginx provides Security by features like SSL/TLS termination, encrypting and decrypting data between clients and servers.
5. Segmentation :- Nginx sends data in smaller chunks.

- Key diffence between apache and nginx is that nginx is fast and its configuration is simple, while apache was realeased a decade ago than nginx so it is slow but apache is extensible. 
- Apache is popular used in most of the servers. The Nginx is gaining popularity in container field as kubernetes uses nginx for ingress.


#### Nginx working

- Nginx conatains 1 master process and multiple worker process.
- Nginx's master process is responsible for reading and validating configuration files and managing worker processes.
- Worker process are the actual process which handles the request.
- The no. of worker process is defined in the conf file.

#### Nginx signal

For  controlling nginx main process uses `nginx -s signal` command to send signals.

- `stop` => fast shutdown
- `quit` => graceful shutdown
- `reload` => reloading the configuration file
- `reopen` => reopening the log files


#### Nginx -s reload

when the user executes the `nginx -s reload` command . A signal for reload is send to the master process. The master process then checks for the configuration files and validates it. If there is error then the configuration rolls back. If the conf file is correct then , at first it send signals to worker process to gracefully stop after finishing the work. And Creates the new working process according to the conf file.


### Nginx -s reload vs systemctl restart nginx

- `Nginx -s reload` does not terminate the master process instead the master process itself reads the new conf file while shutting down the old worker process .
- `systemctl restart nginx` terminates the whole nginx application gracefully then starts the master process which will then read the new conf file.
- `Nginx -s reload` rollbacks if the conf file has error while systemctl has no rlloback feature.  



### Configuration File structure in Nginx

- Conf file consists of modules which are controlled by directives. The directive could be said as simple commands / directions.
- Nginx has simple directives (single line ;)and block directive ({ multiple lines })
- A block directive is called an context if it has other directives inside it. eg: http, server, location, events, etc.
- a directive without any context is inside the main context by default.
- Nginx configuration files are usually located in `/etc/nginx`.

####  Server Blocks 
 Server blocks allows us to configure settings for individual domains or subdomains.

### Location block in nginx

- Location block is used to configure based on request URI. 
- It matches the incoming normalized URI with the pattern and reacts based on the configuration. 
- A location can be either defined by a prefix string or by regular expression. 
- The regular expression starts with `~` for case sentive or `~*` for case insensitive.
- To find the location of given request the nginx first checks the prefix string . the longest prefix is rememberd . 
- Then it matches the regular expression in order if found the the first one is  used .
- If not found then the prefix string which was rememberd will be used.
- They are nested within server blocks and are crucial for applying specific settings to different parts of the website.



### Access log and error log

- If access log and error log is enabled then logs could be found in `/var/log/nginx`
- The access logs are those nginx logs which are used to record the activities of all the visitors of the site.
- The access log is used to analyze the traffic and monitor how users are behaving on our site.
- We can enable access logs by 
```
http {
      ...
      access_log  /var/log/nginx/access.log;
      ...
}
```

- The error logs are the one which records any errorful event the nginx faces.
- The errors may happen when there are errors in configuration file.
- It can enabled by
```
http {
      ...
	  error_log  /var/log/nginx/error_log  crit;
	  ...
}
```



![](Images/d7-nginx.png)

### Security headers

- Security headers are the http response headers that helps to protect system by instructing browser how they should handle the content of the site.
- these headers helps protect against cross-site scripting (XSS), clickjacking, code injection, and other potential vulnerabilities.
- Some of the headers are :
	 1. Content-Security-Policy (CSP)
	 2. X-Frame-Options
	 3. X-XSS-Protection
	 4. Strict-Transport-Security (HSTS)
	 5. X-Content-Type-Options
	 6. Referrer-Policy