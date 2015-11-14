---
services: active-directory
platforms: java
author: brandwe
---

# Integrating Azure AD into a Java command line using username and password

This sample demonstrates a command line application calling a web API that is secured using Azure AD. The Java application uses the Active Directory Authentication Library for Java (ADAL4J) to obtain a JWT access token through the OAuth 2.0 protocol. The access token is sent to the web API to authenticate the user. This sample shows you how to use ADAL to authenticate users via raw credentials (username and password) via a text-only interface.


## Quick Start

Getting started with the sample is easy. It is configured to run out of the box with minimal setup.

### Step 1: Register an Azure AD Tenant

To use this sample you will need a Azure Active Directory Tenant. If you're not sure what a tenant is or how you would get one, read [What is an Azure AD tenant](http://technet.microsoft.com/library/jj573650.aspx)? or [Sign up for Azure as an organization](http://azure.microsoft.com/documentation/articles/sign-up-organization/). These docs should get you started on your way to using Azure AD.

### Step 2: Download Java (7 and above) for your platform 

To successfully use this sample, you need a working installation of [Java](http://www.oracle.com/technetwork/java/javase/downloads/index.html) and [Maven](https://maven.apache.org).

### Step 3: Download the Sample application and modules

Next, clone the sample repo and install the project's dependencies.

From your shell or command line:

* `$ git clone https://github.com/Azure-Samples/active-directory-java-native-headless.git`
* `$ cd active-directory-java-native-headless`

### Step 5: Configure your web app using `PublicClient.java`

Enter the client_id and the tenant name values at the top of the `PublicClient.java` file.

### Step 6: Package and then deploy the `public-client-adal4j-sample.jar` file.

From your shell or command line:

* `$ mvn package`

This will generate a `adal4jsample.war` file in your /targets directory. Deploy this war file using Tomcat or any other J2EE container solution. This WAR will automatically be hosted at `http://<yourserverhost>:<yourserverport>/adal4jsample/`

* `$ java -cp  public-client-adal4j-sample.jar PublicClient`


### You're done!

Click on "Sign-in" to start the process of logging in.

### Acknowledgements

We would like to acknowledge the folks who own/contribute to the following projects for their support of Azure Active Directory and their libraries that were used to build this sample. In places where we forked these libraries to add additional functionality, we ensured that the chain of forking remains intact so you can navigate back to the original package. Working with such great partners in the open source community clearly illustrates what open collaboration can accomplish. Thank you!


