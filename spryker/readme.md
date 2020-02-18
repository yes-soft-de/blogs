# a Fast Guide to Install Spryker on Debian/Ubuntu Linux Based Systems

The documentation has changed again in Spryker webpage, and I didn't find it helpful especially for the native installation upon my `linux` system. so in this blog i plan to fix that along with updating the last blog on some changes on the installation process. so here it goes.

## Preface

Spryker is the name of modality, with above 700+ "modules" so far, each one has a specific job in mind connected via `the facade` design pattern. you can find more in their website https://spryker.com .

Note. I'm using a modified version of Debian, but non of the commands is OS version specific, so you can move along with no problem.

## System Requirements

1. JDK (Java Development Kit V8 or Greater, But I recommend 5)
2. Elastic Search 5, and version 5 of it specifically only so far.
3. PostgreSQL 11
4. (Optional) MySQL
5. Jenkins
6. Redis server
7. PHP 7.2+ (I used PHP 7.3 in My installation) along with several extentions
8. Nginx or Apache
9. NodeJS v8 <b>not the pre installed 10 in my case</b> i trick i have is using nvm i will explain next.
10. RabbitMQ



## Installation Process

I will be using a lot of SH/BASH commands, but I will provide the source of that command if possible to make this blog as future proof as possible

### NVM Installation (NodeJS Installation)

from their github repo we can use the following command:

```sh
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.2/install.sh | bash
```

after that we should restart the terminal,

and then we install the proper version for Spryker which is 8.11.4 using the command

```shell
nvm install 8.11.4
```

after some downloading we can use `node -v` to make sure we have the proper version, note that we can switch between versions of node using nvm, which will save us a lot of headache when dealing with different projects.

you can also use the binary package that suites provided by the link https://nodejs.org/en/blog/release/  and use this blog for installing from binaries:  https://github.com/nodejs/help/wiki/Installation 

### Elastic Search Installation

It's really hard to find the release required for Spryker, but you can find it in the link  https://www.elastic.co/downloads/past-releases/elasticsearch-5-6-16  you'll need the `deb` file, you can use `rpm` for fedora and RedHat-Linux Based systems.

To install the package you can execute the following command:

```shell
sudo dpkg -i elasticsearch-5.6.16.deb
```

Now you can start/stop the service using 

```sh
sudo systemctl start elasticsearch.service
sudo systemctl stop elasticsearch.service
```

if the service isn't loaded yet (and it should be) then you'll need to enable the service using 

```sh
sudo /bin/systemctl daemon-reload
sudo /bin/systemctl enable elasticsearch.service
```

### GraphViz Installation 

this one is pretty easy, just install it using apt

```sh
sudo apt install graphviz
```



### RabbitMQ Installation

again using apt

```sh
sudo apt install rabbitmq-server
```



### Redis Server

easy peasy lemons squeezy

```sh
sudo apt install redis-server
```



### PHP with Extensions

if PHP is not installed we'll install `php-fpm` in the system, this is done by executing

```sh
sudo apt install php-fpm
```

note that this is used for Nginx Config, if you plan to use Apache2 then the command would be

```sh
sudo apt install php libapache2-mod-php
```

heck the version of PHP using `php --version`it should be above 7.2+, if not use the following blog post to upgrade PHP, now in my system it's 7.3.12

to install all the extensions needed just execute the command

```sh
sudo apt install php-curl php-json php-mysql php-pdo-sqlite php-sqlite3 php-gd php-intl php-mysqli php-pgsql php-ssh2 php-gmp php-mcrypt php-pdo-mysql php-readline php-twig php-imagick php-memcache php-pdo-pgsql php-redis php-xml php-bz2 php-mbstring

```

if the `pdo` `sql` dependencies are not working or displaying an error, just delete them.

### Cloning B2B/B2C Shops

choose a directory that suits you and clone either one of these repos. i choose B2C and cloned it in the `~/spryker` directory, so get used to it :) 

this is done using the command (for completion sake)

```sh
git clone https://github.com/spryker-shop/b2c-demo-shop.git
```



### Installing Jenkins

first we should enable Jenkins PPA using the commands

```sh
wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
```

then we should update the apt list and add install Jenkins

```sh
sudo apt update
sudo apt install jenkins
```

and voila, Jenkins is installing.

you'll need now to unlock it but I'll save that to the config stage.



## Configuring the System

this is done in any order you like.

### Starting Services

```sh
sudo systemctl start elasticsearch.service
sudo systemctl start jenkins
sudo systemctl start redis-server
sudo systemctl start rabbitmq-server
```



### Configuring Jenkins

first edit the port used by Jenkins by editing the file located in: `/etc/default/jenkins` and change the port located their from 8080 to 10007.

`HTTP_PORT=8080` => `HTTP_PORT=10007`.

restart the service using 

```sh
sudo systemctl restart jenkins
```

then use 

```sh
sudo less /var/lib/jenkins/secrets/initialAdminPassword
```

you'll get a password their copy it and use it to start Jenkins.

then head to `localhost:10007` using your browser and past that password.



### Configurating Elastic Search

execute the following command

```sh
sudo vi /etc/elasticsearch/elasticsearch.yml
```

then uncomment the part in network about the port and change the port to 

```yaml
http.port: 10005
```



### Configurating Redis

make sure that the used port is `10009`, you can find this setting in the file `/etc/redis/redis.conf` and it's located in a section called network in the line about 69.



### RabbitMQ

first enable admin ui

```sh
rabbitmq-plugins enable rabbitmq_management
```

then start the server

```sh
sudo systemctl start rabbitmq-server
```

then go to the link: `localhost:15672`, use `guest` as both a username and a password

1.  Go to admin tab 
2.  Go to virtual hosts and add the following:
   1. AT_development_zed
   2. DE_development_zed
   3. US_development_zed
3.  The final product should be something like this 

https://yes-soft.de/wp-content/uploads/2019/11/1-2.png

4.  Go to users and add the following 
   1. AT_development” as “management” with password `mate20mg`
   2. “DE_development” as “management” with password `mate20mg`
   3. “US_development” as “management” with password `mate20mg`
   4. “admin” as “administrator” with password `mate20mg`
5. The final product should be something like this

https://yes-soft.de/wp-content/uploads/2019/11/2.png

Aaaaand we're done for the most part, what remains is just installing the B2C repo.


### Correcting config files

there might be some errors with RabbitMQ Permissions, this is due to a config problem where an unnecessary "/" exists, to fix this download the config from this link:

https://drive.google.com/open?id=1ghpGRKbr55SW3g3RiSpCOV60ECS9vpX5

and replace the files exists in `config/Shared` folder or remove "/" yourself from every RabbitMQ config in the folder.


## Installing the Software

execute the following command in the repository.

```sh
ulimit -n 65535
vendor/bin/install -r development
```



### Configuring Nginx

use the following Nginx config:

#### for Yves

the original file is located under: 

```
location / {
    if (-f $document_root/maintenance.html) {
        return 503;
    }

    if ($http_origin ~* "^(http|https)://(img[1234]|cdn|static|cms)\.") {
      add_header "Access-Control-Allow-Origin" $http_origin;
    }

    if ($request_method = OPTIONS) {
        return 200;
    }

    add_header X-Server $hostname;
    try_files $uri @rewriteapp;
}

location @rewriteapp {
    # rewrite all to app.php
    rewrite ^(.*)$ /index.php last;
}


```



#### for Zed

```
proxy_read_timeout 600s;
proxy_send_timeout 600s;
fastcgi_read_timeout 600s;
client_body_timeout 600s;
client_header_timeout 600s;
send_timeout 600s;

location ~ (/images/|/scripts|/styles|/fonts|/bundles|/favicon.ico|/robots.txt) {
    access_log        off;
    expires           30d;
    add_header Pragma public;
    add_header Cache-Control "public, must-revalidate, proxy-revalidate";
    try_files $uri =404;
}

location /payone/ {
    auth_basic off;
    add_header X-Server $hostname;
    try_files $uri @rewriteapp;
}

location / {
    try_files $uri @rewriteapp;
}

location @rewriteapp {
    # rewrite all to app.php
    rewrite ^(.*)$ /index.php last;
}

```









