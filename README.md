Lizmap
======

 

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
wget -P /home/GeoPoppy https://raw.githubusercontent.com/geodatup/docker-lizmap-odroidC2/lz3.1_qgs2.14.11/docker-compose.yml
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

 

 

 

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
docker run --restart="always" --name "lizmap" -p 80:80 -d -t -v /home/GeoPoppy/lizmap/project:/home -v /home/GeoPoppy/lizmap/lizmap_project/lizmap_var:/var/www/websig/lizmap/var geopoppy_lizmap
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
