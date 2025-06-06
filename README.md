# keycloak-user-storage-spi
user-storage-jpa: User Storage Provider with JPA
Level: Beginner
Technologies: JPA
Summary: User Storage Provider with JPA
Target Product: Keycloak
Source: https://github.com/keycloak/keycloak-quickstarts

What is it?
This is an example of the User Storage SPI implemented using JPA. It shows you how you might use these components to integrate Keycloak with an existing external custom user database. The example integrates with a simple relational database schema that has one user table that stores a username, email, phone number, and password for one particular user. Using the User Storage SPI this table is mapped to the Keycloak user metamodel so that it can be consumed by the Keycloak runtime. Before using this example, you should probably read the User Storage SPI chapter of our server developer guide.

System Requirements
You need to have Keycloak running. It is recommended to use Keycloak 22 or later.

All you need to build this project is Java 17 (Java SDK 17) or later and Maven 3.6.3 or later.

Build and Deploy the Quickstart
You must first configure the datasource it uses. For that, copy the conf/quarkus.properties to the conf directory of the server distribution. In this file, you have a named datasource using the same name as the persistence unit from the quickstart. By using the same name, you make sure the persistence unit will be using the correct datasource.

To build the provider, run the following maven command:

mvn -Pextension clean install -DskipTests=true
To install the provider, copy the target/user-storage-jpa-example.jar JAR file to the providers directory of the server distribution.

Finally, start the server as follows:

kc.[sh|bat] start-dev
Enable the Provider for a Realm
Login to the Keycloak Admin Console and got to the User Federation tab. You should now see your deployed provider in the add-provider list box. Add the provider, save it. This will now enable the provider for the 'master' realm. Because this provider implements the UserRegistrationProvider interface, any new user you create in the admin console or on the registration pages of Keycloak, will be created in the custom store used by the provider. If you go to the Users tab in the Admin Console and create a new user, you'll be able to see the provider in action.

Integration test of the Quickstart
Make sure you have a Keycloak server running with the installed provider, the quarkus.properties file and with an administration user with username admin and password admin in the master realm. Your Keycloak server should be listening on http://localhost:8180. You can archive this by running:
./kc.sh start-dev --http-port=8180
You need to have Chrome browser installed and updated to the latest version. See README for additional details.
Run mvn clean install -Dextension
More Information
The User Storage SPI and how you can use it is covered in detail in our server developer guide.
