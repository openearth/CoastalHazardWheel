Containers and linking images:


General: Install dockerhub on windows: https://docs.docker.com/docker-for-windows/install/

PYWPS processes and container creation
--Created git repo on Openearth: https://github.com/openearth/CoastalHazardWheel.git
--The master branch contains pywps python code. This contains a 'processes' folder in which you
  can add the processes you need.
--Work method: Clone repo, add processes, push to repo.
--Docker container is created by entering \docker\ubuntu\flask in windows powershell and running:
	docker build -t pywps/flask-ubuntu:latest .
--Check that the image is there by doing: docker images
--Run the docker container with:
	docker run -p 5000:5000 pywps/flask-ubuntu
--Once running, navigate to localhost:5000


*************************************************************

The postgres docker image can be pulled from dockerhub:
--The container is located at https://hub.docker.com/_/postgres and can be pulled
  from the powershell with the command: docker pull postgres
  
however, postgis seems to be a better option, this can be obtained from https://hub.docker.com/r/kartoza/postgis/
*************************************************************

The geoserver can be pulled from dockerhub:
--The container is located at https://hub.docker.com/r/geonode/geoserver
--Recommended installation is to pull with docker pull geonode/geoserver

Alternatively download this pywps.tar file; Open windows power shell, navigate to where you saved the file and run: docker load -i geoserver.tar.
Now run 'docker images' to ensure you have the image geonode/geoserver available. 

Unzip data-2.15.x.zip. This contains data needed by the docker container. (This can also be obtained from https://build.geo-solutions.it/geonode/geoserver/latest/)

Run the geoserver with the following command in windows powershell:
docker run --name "geoserver" -v /var/run/docker.sock:/var/run/docker.sock -v D:\PROJECTS\CHW_pywps\data-2.15.x\data\:/geoserver_data/data -p 8080:8080 geonode/geoserver

You'll need to change D:\PROJECTS\CHW_pywps\data-2.15.x\data\ to the path where you unzipped the data-2.15.x.zip folder.

Give it about 45 seconds and then navigate to http://localhost:8080/geoserver in your web browser. Log in with username: admin password: geoserver

--instead of mounting with the -v command the geoserver can be linked to the postgis kartoza database with a --link command added to the docker run command.

****************************************************************************************************************

Frontend docker has not been created. I don't know where the front end is.
****************************************************************

AWS:

Documentation for running geoserver on AWS: 
https://cloudinfrastructureservices.co.uk/how-to-setup-geoserver-on-windows-in-azure-aws-gcp/
https://remotely360.com/blog/geospatial-location-intelligence/geoserver-postgis-aws
The last one seems to be the best link. This will also solve the issue of connecting the geoserver with postgis.

