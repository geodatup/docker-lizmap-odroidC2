odroid C2 - docker-lizmap
=========================

 

 

~   docker\_lizmap

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

Go to the doc (in french) for global installation of standalone server WebGIS
with Docker, Postgresql/Postgis, Qgis-server and lizmap :

[RTD](http://cartodroid.readthedocs.io/en/latest/)

LizMap is a complete QGIS webmap's publishing. It’s OpenSource. Many feature as
editing and map printing.

 

LizMap est une solution complète de publication de cartes QGIS sur Internet.
Open source, Lizmap contient des fonctionnalités d’éditions de données et
d’impressions de carte.

 

lizmap-plugin-master / lizmap-web-client-3.0.1 / qgis-server-2.14.4
===================================================================

First, install docker on odroid C2 :

https://github.com/geodatup/[cartodroid](https://github.com/geodatup/cartodroid)/[script](https://github.com/geodatup/cartodroid/tree/master/script)/**install\_docker\_C2.sh**

then QgisServer and Lizmap containers :

 

and install Postgresql-postgis:

https://github.com/jancelin/docker-postgis-rpi

![docker\_lizmap](https://cloud.githubusercontent.com/assets/6421175/12889497/6c3a926e-ce7f-11e5-8391-de6b205307e2.png)

This image contains a WebGIS server: Apache, qgis-mapsever, lizmap-web-client,
and all dependencies required for operation

To build the image do:

you can build an image from Dockerfile:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
docker build -t jancelin/rpi-docker-lizmap git://github.com/jancelin/rpi-docker-lizmap
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

2.before the first running :

-   Create folder for persistent data and config

    ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    mkdir /home/lizmap_var
    mkdir /home/lizmap_project 
    ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-   set rights on lizmap\_project

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
chown :www-data -R /home/lizmap_project
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-   Copy files .qgs et .qgs.cfg in /home/lizmap\_project (you can do after)

-   run a container with volume lizmap\_var for copy /var/lizmap:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
docker run --name "lizmap_temp" -p 8081:80 -d -t -v /home/test:/home lizmap
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-   go into lizmap\_temp container:

`docker exec -it lizmap_temp bash`

-   Copy folders with rights lizmap/var:

`cp -avr /var/www/websig/lizmap/var /home`

-   exit container:

`exit`

-   On host, delete lizmap\_temp

`docker stop lizmap_temp && docker rm lizmap_temp`

-   start final container

`docker run --restart="always" --name "lizmap" -p 80:80 -d -t -v
/home/lizmap_project:/home -v /home/lizmap_var:/var/www/websig/lizmap/var
lizmap`

-   Now config lizmap on web :

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
http://10.10.0.25/websig/lizmap/www/admin.php
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-   Add **/home/** for looking your geo projects

![config](https://cloud.githubusercontent.com/assets/6421175/11306233/e945f342-8fb0-11e5-9906-4010b9398ef1.png)

-   http://docs.3liz.com/fr/

Lizmap working with your data and config at :

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
http://"your_ip_rpi_wifi_serveur"
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

exemple for me: http://10.10.0.25

or

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
http://"your_ip_rpi_wifi_serveur"/websig/lizmap/www/
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

lizmap admin at

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
http://"your_ip_rpi_wifi_serveur"/websig/lizmap/www/admin.php
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Lizmap Web Application generates dynamically a web map application
(php/html/css/js) with the help of Qgis Server ( QGIS Server Tutorial ). You can
configure one web map per Qgis project with the QGIS LizMap Plugin.

http://docs.3liz.com/

http://www.3liz.com/

Julien ANCELIN ( julien.ancelin\@stlaurent.lusignan.inra.fr) 01/2015
