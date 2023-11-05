# Overview
The current GTO server is running on a small ECS Liva mini server at Jenny's house.

The server is running Linux Ubuntu Server with a Docker Engine that runs four containers serving GTO.

Two ports, 443 (https) and 22 (ssh) are exposed by the server and Jenny's house firewall forwards these to the internet. All other ports are blocked.

The server is configured with a Dynamic DNS (with cloudns.net) to the domain name liva.walls.net.nz.  CGC's own DNS name server maps gto.canterburyglidingclub.nz to liva.walls.net.nz.  A cron job on gto_ctrl keeps the dynamic dns up to date.

Https certificates are configured for \*.walls.net.nz and gto.canterburyglidingclub.nz using LetsEncrypt's Certbot to refresh the certificates.

All source files used in GTO can be found in the /var/gto folder. The docker containers mount this directory as an external volume.

# Source code
Code source is in four different repositories (Flightlog,gto2,gto_docker & GTOIdentityService) in https://github.com/AlanWalls/Flightlog.git

Documentation source is in https://github.com/nallison/GTODocTest.git

These repositories have been cloned into /var/gto on the server.  In a "Hit by a bus" scenario, this is the easiest way to get the source. :-)

GTO source is NOT open source, it is owned by Alan Walls (me).  I do grant Canterbury Gliding Club unlimited use of this source for their club use.

The Documentation was largely written by Neil Allison.

# Docker

1) **gto** is the main container that runs an Apache web server with the GTO php (Code Igniter 4.0) application.  This container also serves the gto document web site.

2) **gto_db** is a MariaDb container which runs the SQL database.

3) **gto2** is running the SvelteKit application running on NodeJS.  This container exposes port 3000 which the gto container publishes

4) **gto_ctrl** runs a small number of miscellaneous tasks.  For example, markdown documentation building, nightly emails and GNZ Tracker updates. 