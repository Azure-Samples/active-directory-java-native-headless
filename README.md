---
services: active-directory
platforms: Java
author: xerners
level: 200
client: Java Console Application
service: Microsoft Graph
endpoint: AAD V1
---
# Integrating Azure AD into a Java console application using username and password

## About this sample

### Overview

This sample demonstrates a Java console application calling Microsoft Graph that is secured using Azure Active Directory.

1. The Java application uses the Active Directory Authentication Library for Java (ADAL4J) to obtain a JWT access token through the OAuth 2.0 protocol.
2. The access token is used as a bearer token to authenticate the user when calling the Microsoft Graph.

![Topology](./ReadmeFiles/Java-Native-Diagram.png)

### Scenario: 

This sample shows you how to use ADAL to authenticate users via raw credentials (username and password) via a text-only interface. For more information about how the protocols work in this scenario and other scenarios, see [Authentication Scenarios for Azure AD](https://azure.microsoft.com/documentation/articles/active-directory-authentication-scenarios/).

## How to run this sample

To run this sample, you'll need:

- Working installation of Java and Maven
- An Internet connection
- An Azure Active Directory (Azure AD) tenant. For more information on how to get an Azure AD tenant, see [How to get an Azure AD tenant](https://azure.microsoft.com/en-us/documentation/articles/active-directory-howto-tenant/)
- A user account in your Azure AD tenant. This sample will not work with a Microsoft account (formerly Windows Live account). Therefore, if you signed in to the [Azure portal](https://portal.azure.com) with a Microsoft account and have never created a user account in your directory before, you need to do that now.

## Quick Start

Getting started with the sample is easy. It is configured to run out of the box with minimal setup.

### Step 1: Download Java (7 and above) for your platform

To successfully use this sample, you need a working installation of [Java](http://www.oracle.com/technetwork/java/javase/downloads/index.html) and [Maven](https://maven.apache.org/).

### Step 2:  Clone or download this repository

From your shell or command line:

`git clone https://github.com/Azure-Samples/active-directory-java-native-headless.git `

### Step 3:  Register the sample with your Azure Active Directory tenant

To register the project, you can:

- either follow the steps in the paragraphs below
- or use PowerShell scripts that:
  - **automatically** create for you the Azure AD applications and related objects (passwords, permissions, dependencies)
  - modify the projects' configuration files.

If you want to use this automation, read the instructions in [App Creation Scripts](./AppCreationScripts/AppCreationScripts.md)

#### First step: choose the Azure AD tenant where you want to create your applications

As a first step you'll need to:

1. Sign in to the [Azure portal](https://portal.azure.com).
1. On the top bar, click on your account, and then on **Switch Directory**. 
1. Once the *Directory + subscription* pane opens, choose the Active Directory tenant where you wish to register your application, from the *Favorites* or *All Directories* list.
1. Click on **All services** in the left-hand nav, and choose **Azure Active Directory**.

> In the next steps, you might need the tenant name (or directory name) or the tenant ID (or directory ID). These are presented in the **Properties**
of the Azure Active Directory window respectively as *Name* and *Directory ID*

#### Register the app app (Native-Headless-Application)

1. In the  **Azure Active Directory** pane, click on **App registrations** and choose **New application registration**.
1. Enter a friendly name for the application, for example 'Native-Headless-Application' and select 'Native' as the *Application Type*.
1. For the *Redirect URI*, enter `https://<your_tenant_name>/Native-Headless-Application`, replacing `<your_tenant_name>` with the name of your Azure AD tenant.
1. Click **Create** to create the application.
1. In the succeeding page, Find the *Application ID* value and copy it to the clipboard. You'll need it to configure the configuration file for this project.
1. Then click on **Settings**, and choose **Properties**.
1. Configure Permissions for your application. To that extent, in the Settings menu, choose the 'Required permissions' section and then,
   click on **Add**, then **Select an API**, and type `Microsoft Graph` in the textbox. Then, click on  **Select Permissions** and select **User.Read**.
1. Navigate back to the 'Required permissions' section, and click on **Grant Permissions**

### Step 4:  Configure the sample to use your Azure AD tenant

In the steps below, ClientID is the same as Application ID or AppId.

#### Configure the app project

1. Open the `src\main\java\PublicClient.java` file
1. Find the line `private final static String CLIENT_ID` and replace the existing value with the application ID (clientId) of the `Native-Headless-Application` application copied from the Azure portal.
1. Find the line `private final static String AUTHORITY = "https://login.microsoftonline.com/common/"` and replace the existing value with the tenant id of the account selected. That information can be visualized in App Services' endpoints information.

### Step 5: Run the sample

From your shell or command line:

- `$ mvn package`

This will generate a `public-client-adal4j-sample-jar-with-dependencies.jar` file in your /targets directory. Run this using your Java executable like below:

- `$ java -jar public-client-adal4j-sample-jar-with-dependencies.jar`

### You're done!

Your command line interface should prompt you for the username and password and then access the Microsoft Graph API to retrieve your user information.

### About the code

The code to acquire a token is located entirely in the `src\main\java\PublicClient.Java` file. The Authentication context is created (line 45), passing the Authority(https://login.microsoftonline.com/common/) and an ExecutorService.

`context = new AuthenticationContext(AUTHORITY, false, service);`

A call to acquire the token is made using the Authentication context (line 46), passing in the resource(Microsoft graph), CLIENT_ID(App id of the app that was registered on Azure AD), and the username and password of the user. 

`Future<AuthenticationResult> future = context.acquireToken("https://graph.microsoft.com", CLIENT_ID, username, password, null);`

The result is passed back to the main() function, where then the access token is extracted and passed to the function making the call to Microsoft Graph(line 33)

`String userInfo = getUserInfoFromGraph(result.getAccessToken());`

The access token is then used as a bearer token to call the Microsoft Graph API (line 68)

`conn.setRequestProperty("Authorization", "Bearer " + accessToken);`

## Community Help and Support

Use [Stack Overflow](http://stackoverflow.com/questions/tagged/adal) to get support from the community.
Ask your questions on Stack Overflow first and browse existing issues to see if someone has asked your question before.
Make sure that your questions or comments are tagged with [`adal` `Java`].

If you find a bug in the sample, please raise the issue on [GitHub Issues](https://github.com/Azure-Samples/active-directory-java-native-headless/issues).

To provide a recommendation, visit the following [User Voice page](https://feedback.azure.com/forums/169401-azure-active-directory).

## Contributing

If you'd like to contribute to this sample, see CONTRIBUTING.md

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/). For more information, see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.

## More information

For more information, see ADAL4J [conceptual documentation](https://github.com/AzureAD/azure-activedirectory-library-for-java/wiki). 

For more information about how OAuth 2.0 protocols work in this scenario and other scenarios, see [Authentication Scenarios for Azure AD](http://go.microsoft.com/fwlink/?LinkId=394414).
