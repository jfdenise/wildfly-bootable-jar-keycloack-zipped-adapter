# Keycloak WildFly bootable jar example

WARNING: THIS IS A WORKAROUND TO USE Keycloak 12.0.x with WildFly 23.

Build a bootable JAR containing an application secured with Keycloak.

In order to declare the deployment to be secured with keycloak, the CLI script `../scripts/configure-oidc.cli` is called during packaging.

In order to register the keycloak adapter subsystem, the `adapter-elytron-install.cli` (that is present in the downloaded zipped adapter) is executed.
 
Initial Steps
=======

* Download the keycloak server from: `https://www.keycloak.org/download`
* Start the keycloak server to listen on port 8090: `keycloak/bin/standalone.sh -Djboss.socket.binding.port-offset=10`
* Log into the keycloak server admin console (you will possibly be asked to create an initial admin user) : `http://127.0.0.1:8090/`
* Create a Realm named `WildFly`
* Create a Role named `Users`
* Create a User named `demo`, password `demo`
* Assign the role `Users` to the user `demo`
* Create a Client named `simple-webapp` with Root URL: `http://127.0.0.1:8080/simple-webapp`

* Create a directory in the root of the project named `extras`. It will contain the JBoss Modules required for keycloak.
* Download the zipped keycloak client OIDC adapter from: `https://www.keycloak.org/download`
* Unzip its content in the `extras` directory.

Build and run
========

* To build: `mvn package`
* To run: `mvn wildfly-jar:run`
* Access the application: `http://127.0.0.1:8080/simple-webapp`
* Access the secured servlet.
* Log-in using the `demo` user, `demo` password (that you created in the initial steps).
* You should see a page containing the Principal ID.