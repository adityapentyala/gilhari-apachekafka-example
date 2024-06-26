# Gilhari Setup and Configuration
This file lists out the steps taken to configure the Gilhari microservice along with JDX ORM. In this example, the classes named Employee, InventoryItem and Sale are created and mapped as follows.

## Step 1. Define and compile empty Java (container) class
In `src/main/java/models`, create a class file `JSON_Employee.java` as shown to create a JDX_JSONObject (derived from Software Tree's JDX).\
Similarly, create class files `JSON_InventoryItem.java` and `JSON_Sale.java` in the same location.\
In the `lib/` directory, add the requirements as `.jar` files (here, a json package and `jxclasses.jar`, found in the `libs/` directory of the Gilhari SDK installation).\
In a terminal, `cd` to `./java_src` and run the command `javac -cp "lib/json-20240303.jar:lib/jxclasses.jar" -d bin src/main/java/models/JSON_Employee.java`. Repeat the same for the other 2 files.

## Step 2. Define a declarative Object Relational Mapping (ORM) specification and Gilhari configuration
In `config/`, create a file named `java_src.jdx` as shown. (This example uses a postgresql database running outside of the Gilhari microservice docker container).\
Also add to `config/` the database's (here, postgresql's) JDBC driver as a `.jar`.\
Add a file `classNameMapping.js` to `config/` to map "Employees" to the defined Employee container class. Repeat the same for the other 2 classes as shown.\
Finally, to `java_src/`, add a file `gilhari_service.config` and fill in the required fields. Refer to the Gilhari documentation for more information on the `.config` file and its fields.

## Step 3. Create a Dockerfile, build and run the container
Create the Dockerfile as shown and run the command
`docker build -t my_app_gilhari -f ./Dockerfile .` to build the docker image.\
Run the image using the command `docker run -p 80:8081 my_app_gilhari`

