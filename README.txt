Steps used during the demo:

== Simple Docker ==

docker run centos:6 cat /etc/redhat-release
docker run -ti centos:6 bash

== Docker Hub ==

docker pull ubuntu
docker run -ti ubuntu bash
apt-get update
apt-get install figlet
figlet "docker is nice"
docker commit -m 'figlet app' -a 'Ricardo Melo' <CONTAINER ID> rjsmelo/figlet-docker
docker push rjsmelo/figlet-docker

== Docker Compose ==

docker-compose build
docker-compose up
docker-compose up -d
browser (fireproxy) -> x.p55 -> x.p56 -> x.p70

== Wordpress ==
unzip wordpress into the sites folder

docker-compose run php55 bash
mysql -h mysql -u root -p
create database wordpress;

- install using interface
cd sites/wordpress/wp-content/themes/twentysixteen/
vim header.php (search get_header_image) and add:

<h1 style="background-color:red;"><?php echo phpversion(); ?></h1>

== Cleanup ==
docker-compose kill
docker-compose rm


