# Cacti docker container

![Cacti](https://raw.githubusercontent.com/oemunoz/cacti/master/images/cacti.png)

Cacti is a complete network graphing solution designed to harness the power of RRDTool's data storage and graphing functionality. Cacti provides a fast poller, advanced graph templating, multiple data acquisition methods, and user management features out of the box. All of this is wrapped in an intuitive, easy to use interface that makes sense for LAN-sized installations up to complex networks with hundreds of devices.

[[http://www.cacti.net]]
## To run the image:

### To run the default image (new Install):
When you run this docker with the basic minimum options:

~~~~bash
docker run -d -p 80:80 oems/cacti
~~~~

- Run out of the box, to install Cacti page.
- Run the Version of Cacti, from the website tar.gz.
- Run with PHP 5 (Developer tested).
- A new WikkaWiki database over MySql 5.5 (tested), with the next DB/user/password options.

The default database:
~~~~text
cacti
~~~~

default user:
~~~~text
cactiuser
~~~~

default password:
~~~~text
cactiuser
~~~~
With this default option, you run the database into the container, then **if you delete your container you delete your database also**, remember to make backup.

### Using your own database files

The internal database use MySql 5.5, using your own database (make backup of your original database before to load this docker):

~~~~bash
docker run -d -p 80:80 -v $PWD/mysql:/var/lib/mysql oems/cacti
~~~~

### Using your own database and your own configuration file.

You can use your own configuration options.

~~~~bash
docker run -d -p 80:80 -v $PWD/mysql:/var/lib/mysql -v $PWD/config.php:/var/www/html/cacti/include/config.php oems/cacti
~~~~
If you use a external database you dont need the mysql volume.

~~~~bash
docker run -d -p 80:80 -v $PWD/config.php:/var/www/html/cacti/include/config.php oems/cacti
~~~~
### Using your own rras files also:

~~~~bash
docker run -d -p 80:80 -v $PWD/mysql:/var/lib/mysql -v $PWD/config.php:/var/www/html/cacti/include/config.php -v $PWD/rra:/var/www/html/cacti/rra oems/cacti
~~~~

### Build your own:

Modify the mysql_wikkawiki.sql with your own user and database definitions and build the image:
~~~~bash
git git@github.com:oemunoz/cacti.git cacti
cd cacti
docker build -t "cacti" .
~~~~

## History

- 161104: Basic Initial Version.
- 161110: Cact now uses root and supervisord for every thing, but must works out of the box. (include crontab, mysql, apache services)

## Credits

All Cacti develops.
[[http://www.cacti.net/donate.php]]
Thanks all them.

## License

GNU General Public License
