# npm node with Nginx installation on UBUNTU

npm node installation on UBUNTU

## Getting Started

These instructions contains commands to install npm and node

### Prerequisites

Create an EC2 instance and RDS instance on AWS

## Installation

open ec2 ubuntu using putty

run the below commands

### Install Nginx

1. `sudo apt-get update && sudo apt-get upgrade -y`

1. `sudo apt-get install nginx -y` 

### Setup Nginx

1. To check the status of nginx  `sudo systemctl status nginx`

1. To start Nginx `sudo systemctl start nginx`

### Install node js

1. `sudo apt-get update`

1. `curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -`

1. `sudo apt-get install -y nodejs`

### Set reverse proxy for nodejs

1. `sudo rm /etc/nginx/sites-available/default`

1. `sudo nano /etc/nginx/sites-available/default`

1. Add the following code to the file and replace private ip address and domain name.
```
server {
    listen 80;
    server_name your_domain.com;
    location / {
        proxy_pass http://private_ip_address:8080;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
     }
}
```

1. For multiple servers in node js use the below code for second route in the same server block
```
location /api {
        rewrite ^/api(.*) /$1 break;
        proxy_pass http://private_ip_address:8081;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
     }

  
```

1. check the syntax error if you made any `sudo nginx -t`
* you will see the following lines
```nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
```

1. Reload the server `sudo /etc/init.d/nginx reload`

1. To restart the server `sudo service nginx restart`

1. Make a directory `NameOfDir`

1. go to directory `cd NameOfDir`

1. To start node project do : `npm init`

1. create a file `touch server.js`

1. open the file `sudo nano server.js`

1. To install any package:  `npm i PACKAGE-NAME --save`

1. If you have package.json with dependencies then: `npm install`

1. install express:  `sudo npm i express --save` 

1. install nodemon:  `sudo npm i -g nodemon` 

1. install helmet to protect your app from well-known web vulnerabilities :  `sudo npm install --save helmet` 

1. create .env:  `touch .env`   , put all your secrets in .env file

1. install dotenv:  `npm i dotenv --save` 



## Authors

* **Navjot** - [Website]

## License

This project is licensed under the MIT Privacy Policy - see our [Privacy and Policies] file for details

## Acknowledgments

* None
