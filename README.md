# Alfresco AIO Project - SDK 4.5

After cloning this repo, perform a mvn package to create JARS using the as-built configuration.

the share jar is located in: custommodel-share/target/custommodel-share-1.0-SNAPSHOT.jar

the content(platform) jar is located in: custommodel-platform/target/custommodel-platform-1.0-SNAPSHOT.jar

refer to this tutorial to setup custom models:
https://docs.alfresco.com/content-services/7.3/tutorial/platform/content-model/#adding-an-association


The solution creates a custom model for whitepapers and a related type for associations.  

After importing the jar files, upload a document in to alfresco and change the type to white paper.

The association is made via rest api call.  here's a CURL to illustrate how the REST api call is made:


curl -X POST "http://3.90.226.222/alfresco/api/-default-/public/alfresco/versions/1/nodes/06783619-6ba7-41e3-a01b-3763eebf0bde/targets" -H "accept: application/json" -H "authorization: Basic ZGVtbzpkZW1v" -H "Content-Type: application/json" -d "{ \"targetId\": \"e2202396-2665-40cc-878d-a63941a54ef6\", \"assocType\": \"my:relatedDocuments\"}"


However you can manually select the associated document in the "edit properties" screen.

Once the associated doc is applied, you can click on the doc in the edit properties window to view it.

# DEFAULT INFO BELOW

This is an All-In-One (AIO) project for Alfresco SDK 4.5.

Run with `./run.sh build_start` or `./run.bat build_start` and verify that it

 * Runs Alfresco Content Service (ACS)
 * Runs Alfresco Share
 * Runs Alfresco Search Service (ASS)
 * Runs PostgreSQL database
 * Deploys the JAR assembled modules
 
All the services of the project are now run as docker containers. The run script offers the next tasks:

 * `build_start`. Build the whole project, recreate the ACS and Share docker images, start the dockerised environment composed by ACS, Share, ASS and 
 PostgreSQL and tail the logs of all the containers.
 * `build_start_it_supported`. Build the whole project including dependencies required for IT execution, recreate the ACS and Share docker images, start the 
 dockerised environment composed by ACS, Share, ASS and PostgreSQL and tail the logs of all the containers.
 * `start`. Start the dockerised environment without building the project and tail the logs of all the containers.
 * `stop`. Stop the dockerised environment.
 * `purge`. Stop the dockerised container and delete all the persistent data (docker volumes).
 * `tail`. Tail the logs of all the containers.
 * `reload_share`. Build the Share module, recreate the Share docker image and restart the Share container.
 * `reload_acs`. Build the ACS module, recreate the ACS docker image and restart the ACS container.
 * `build_test`. Build the whole project, recreate the ACS and Share docker images, start the dockerised environment, execute the integration tests from the
 `integration-tests` module and stop the environment.
 * `test`. Execute the integration tests (the environment must be already started).

# Few things to notice

 * No parent pom
 * No WAR projects, the jars are included in the custom docker images
 * No runner project - the Alfresco environment is now managed through [Docker](https://www.docker.com/)
 * Standard JAR packaging and layout
 * Works seamlessly with Eclipse and IntelliJ IDEA
 * JRebel for hot reloading, JRebel maven plugin for generating rebel.xml [JRebel integration documentation]
 * AMP as an assembly
 * Persistent test data through restart thanks to the use of Docker volumes for ACS, ASS and database data
 * Integration tests module to execute tests against the final environment (dockerised)
 * Resources loaded from META-INF
 * Web Fragment (this includes a sample servlet configured via web fragment)

# TODO

  * Abstract assembly into a dependency so we don't have to ship the assembly in the archetype
  * Functional/remote unit tests
