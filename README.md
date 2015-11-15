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

### Step 4: Register the GraphClient app

* Sign in to the Azure management portal.
* Click on Active Directory in the left hand nav.
* Click the directory tenant where you wish to register the sample application.
* Click the Applications tab.
* In the drawer, click Add.
* Click "Add an application my organization is developing".
* Enter a friendly name for the application, for example "GraphAPI-Headless-Java", select "Native Client Application", and click next.
* For the Redirect URI, enter http://GraphClient. Please note that the Redirect URI will not be used in this sample, but it needs to be defined nonetheless. Click finish.
* Click the Configure tab of the application.
* Find the Client ID value and copy it aside, you will need this later when configuring your application.
* In "Permissions to Other Applications", ensure "Windows Azure Active Directory" is selected. Select "Sign in and read user profile" from the "Delegated Permissions" dropdown and ensure it is checked. This will be the permission we'll be using in the sample.


### Step 5: Configure your web app using `PublicClient.java`

Enter the client id value above at the top of the `PublicClient.java` file.

```java
public class PublicClient {

    private final static String AUTHORITY = "https://login.microsoftonline.com/common/";
    private final static String CLIENT_ID = "<your client id>";

```

### Step 6: Package and then run the `public-client-adal4j-sample-jar-with-dependencies.jar ` file.

From your shell or command line:

* `$ mvn package`

This will generate a `public-client-adal4j-sample-jar-with-dependencies.jar` file in your /targets directory. Run this using your Java executable like below:

* `$ java -cp  public-client-adal4j-sample-jar-with-dependencies.jar  PublicClient`


### You're done!

Your command line interface should prompt you for the username and password and then access the Graph API to retreive your user information.

### Acknowledgements

We would like to acknowledge the folks who own/contribute to the following projects for their support of Azure Active Directory and their libraries that were used to build this sample. In places where we forked these libraries to add additional functionality, we ensured that the chain of forking remains intact so you can navigate back to the original package. Working with such great partners in the open source community clearly illustrates what open collaboration can accomplish. Thank you!


