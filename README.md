marcelorodrigo/apache-php-kohana
================================

Base docker image to run legacy Kohana PHP 2.3.x applications on Apache / PHP 5.3

[![Docker Stars](https://img.shields.io/docker/stars/marcelorodrigo/apache-php-kohana.svg?maxAge=2592000)]()
[![Docker Pulls](https://img.shields.io/docker/pulls/marcelorodrigo/apache-php-kohana.svg?maxAge=2592000)]()
[![](https://images.microbadger.com/badges/image/marcelorodrigo/apache-php-kohana.svg)](http://microbadger.com/images/marcelorodrigo/apache-php-kohana)
[![We love bikes](https://img.shields.io/badge/we%20love-bikes-orange.svg)]()


Running your Kohana-2.3.x docker image
--------------------------------------

Start your image binding the external ports 80 in all interfaces to your container:

    docker run -ti -p 80:80 marcelorodrigo/apache-php-kohana


Mapping your Kohana application
-------------------------------

If you are using this image, probabily you have a legacy Kohana 2.3.x application.
So it's time to map a volume for your app:

    docker run -ti -p 80:80 -v /your-app-folder:/app marcelorodrigo/apache-php-kohana


Configuring your document root
------------------------------

By default this image looks for a folder named "public_html" inside your project root folder.
You can customize using DOCUMENTROOT enviroment variable:

    docker run -ti -p 80:80 -v /your-app-folder:/app -e "DOCUMENTROOT=web" marcelorodrigo/apache-php-kohana

Loading your Kohana application inside the image
-----------------------------------------------

This image can be used as a base image for your application.
Create a new `Dockerfile` in a new folder and put your Kohana root folder with the following contents:

    FROM marcelorodrigo/apache-php-kohana
    RUN rm -rf /app
    ADD . /app

After that, build the new `Dockerfile`:

    docker build -t myuser/my-kohana-app .

And test it:

    docker run -d -p 80:80 myuser/my-kohana-app
