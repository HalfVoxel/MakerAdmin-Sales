Sales service
=============
Gives the ability to create products and sell them and make payments.


Installation
============
The following guide will help you install the Sales module. Before installning this module you should make sure the API Gateway module is up and runing, as this is required to be able to run other services in the system.

# Requirements
* A working MySQL server
* The API Gateway should already be up and running

# Step 1: Download the source code from GitHub
```
git clone https://github.com/MakersOfSweden/MakerAdmin-Sales
cd ./MakerAdmin-Sales/docker/
```

# Step 2: Create a database
Create a new database and user in your MySQL database server.

```
CREATE USER `makeradmin-sales`@'%' IDENTIFIED BY 'password';
CREATE DATABASE `makeradmin-sales`;
GRANT ALL ON `makeradmin-sales`.* TO `makeradmin-sales`@'%';
FLUSH PRIVILEGES;
```

# Step 3: Build docker container
The following script will build a new docker container and tag it with the correct name and version.
```
./docker_build
```

# Step 4: Start docker container
You can now start an instance of the Sales module and register it in the MakerAdmin system. Make sure you specify the database credentials specified in step 2. The last parameter should be the address to the API gateway. Keep in mind that this is the hostname provided by Docker, so it should be the same as the name of the container.
```
./docker_run mysql makeradmin-sales password makeradmin-sales makeradmin-apigateway
```

# Step 5: Create database tables
To create the database table you have to run the migration scripts.
```
./artisan migrate
```

# Step 6: Test the service
The service should now be up and running and should be possible to access from the API.