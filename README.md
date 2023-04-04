# assignment-1-part-3

# Step-1 Create a new Docker volume named "my_volume". 

# Command To Exec
docker volume create my_volume
	 
# Output 
my_volume
	 
# Step-2 Create a new Docker container using the "nginx" image and mount the "my_volume" volume to the container's "/usr/share/nginx/html" directory.

# Command To Exec
docker run -d -p 8080:80 --name my_nginx_container -v my_volume:/usr/share/nginx/html nginx

# Output
595b6bab45be9a77cc94b035de8569eb9511d67951f85d60628a7cc1b4eda730	

# What the command is 
Here, we are running a new Docker container with the name "my_nginx_container", using the "nginx" image. We are also mapping port 80 of the container to port 8080 of the host machine using the "-p" option. The "-v" option is used to mount the "my_volume" volume to the "/usr/share/nginx/html" directory of the container. The "-d" option is used to run the container in detached mode.

# Step-3 Verify that the "nginx" default page is accessible on your host machine at http://localhost:8080.

For this step we just need to browse the URL http://localhost:8080 on our local machine ( Any Browser ).

# Step-4 Create a new file named "index.html" on your host machine and add some text to it.

# Command To Exec
nano index.html 

this will open a file in editor & we can write any desired text.

Then will press CTRL + X & CTRL + Y & Then Click Enter.

# Step-5 Copy the "index.html" file from your host machine to the "my_volume" volume using the "docker cp" command.

# Command To Exec
docker cp index.html my_nginx_container:/usr/share/nginx/html

# Output 
Successfully copied 2.048kB to my_nginx_container:/usr/share/nginx/html

# What The Command Is
Here, index.html is the file name and my_nginx_container is the name of the Docker container we created in the previous step.

# Step-6 Verify that the "index.html" file is accessible on your host machine at http://localhost:8080.

For this repeat step 3.

# Step-7 Stop and remove the container.

We dont need to stop or remove the container here because it is being used in the below steps, if we stop it for this step we will need to restart the container to be able to move forward it steps below.

Just for Reference, The Command to Stop is
docker stop <container_name>

& to Remove
docker rm <container_name>

# Step-8 Create a new Docker container using the "httpd" image and mount the "my_volume" volume to the container's "/usr/local/apache2/htdocs" directory.

# Command To Exec
docker run -d -p 8081:80 --name my_httpd_container -v my_volume:/usr/local/apache2/htdocs httpd

# Output
20478528e81d15ffdd41030093699a7bc004806009239448f6a1d7db5b1904fb

# Step-9 Verify that the "httpd" default page is accessible on your host machine at http://localhost:8081.

For This repeat the step 3 just make sure this time the URL is having 8081 instead of 8080.

# Step-10 Create a new file named "about.html" on your host machine and add some text to it.

# Command To Exec
nano about.html

this will open a file in editor & we can write any desired text.

Then will press CTRL + X & CTRL + Y & Then Click Enter.

# Step-11 Copy the "about.html" file from your host machine to the "my_volume" volume using the "docker cp" command.

# Command To Exec
docker cp about.html my_nginx_container:/usr/share/nginx/html/about.html

# Output
Successfully copied 2.048kB to my_nginx_container:/usr/share/nginx/html/about.html

# Step-12 Verify that the "about.html" file is accessible on your host machine at http://localhost:8081/about.html.

For this will repeat the step 3 but just with the above URL having /about.html

# Step-13 Stop and remove the container.

We dont need to stop or remove the container here because it is being used in the below steps, if we stop it for this step we will need to restart the container to be able to move forward it steps below.

Just for Reference, The Command to Stop is
docker stop <container_name>

& to Remove
docker rm <container_name>

# Step-14 Verify that the "index.html" and "about.html" files are still available in the "my_volume" volume.

# Command To Exec
docker exec -it my_nginx_container ls /usr/share/nginx/html

# Output
50x.html  about.html  index.html

# Step-15 Cleanup: Remove the "my_volume" volume.

# Command To Exec
docker volume rm my_volume

# Output
my_volume

