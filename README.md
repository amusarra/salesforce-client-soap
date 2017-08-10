
# Salesforce SOAP API Client OSGi Bundle
[![Antonio Musarra's Blog](https://img.shields.io/badge/maintainer-Antonio_Musarra's_Blog-purple.svg?colorB=6e60cc)](https://www.dontesta.it)
[![Build Status](https://travis-ci.org/amusarra/salesforce-client-soap.svg?branch=master)](https://travis-ci.org/amusarra/salesforce-client-soap)
[![Maven Central](https://maven-badges.herokuapp.com/maven-central/it.dontesta.labs.liferay.salesforce.client.soap/salesforce-client-soap/badge.svg)](https://search.maven.org/#artifactdetails%7Cit.dontesta.labs.liferay.salesforce.client.soap%7Csalesforce-client-soap%7C1.0.2%7Cjar)
[![](https://img.shields.io/badge/download-OSGi%20Bundle-green.svg)](http://repo1.maven.org/maven2/it/dontesta/labs/liferay/salesforce/client/soap/salesforce-client-soap/1.0.2/salesforce-client-soap-1.0.2.jar)
[![Twitter Follow](https://img.shields.io/twitter/follow/antonio_musarra.svg?style=social&label=%40antonio_musarra%20on%20Twitter&style=plastic)](https://twitter.com/antonio_musarra)

This project implements an OSGi bundle to interact with Salesforge SOAP APIs. The OSGi bundle is created through 
the **Force.com Web Service Connector (WSC) version 40.1.1** and export this package:

1. com.sforce.soap.partner.*
2. com.sforce.soap.enterprise.*
2. com.sforce.ws.*

This Salesforce SOAP API Client Bundle can be installed in **every [OSGi R6](https://www.osgi.org/developer/downloads/release-6/) compliant container**.

Salesforce provides two different SOAP API WSDLs:
1. Enterprise WSDL
2. Partner WSDL

**Enterprise Web Services WSDL** used by enterprise developers to build client applications for a single Salesforce organization. 
The enterprise WSDL is strongly typed, which means that it contains objects and fields with specific data types, 
such as ``int`` and ``string``. 

*Customers who use the enterprise WSDL document must download and re-consume it when 
changes are made to the custom objects or fields in their org or when they want to use a different version of the API.* 

To access the current WSDL for your organization, log in to your Salesforce organization and from Setup, enter 
Generate Enterprise WSDL in the Quick Find box, then select **Generate Enterprise WSDL**.

**Partner Web Services WSDL** used for client applications that are metadata-driven and dynamic in nature. 
It is particularly—but not exclusively—useful to Salesforce partners who are building client applications for 
multiple organizations. As a loosely typed representation of the Salesforce data model that works with 
name-value pairs of field names and values instead of specific data types, it can be used to access data 
within any organization. 

*This WSDL is most appropriate for developers of clients that can issue a query call to get information 
about an object before the client acts on the object. __The partner WSDL document needs to be downloaded and 
consumed only once per version of the API__.* 

To access the current WSDL for your organization, log in to your Salesforce organization and from Setup, 
enter Generate Partner WSDL in the Quick Find box, then select **Generate Partner WSDL**.

This Salesforce SOAP API Client Bundle __use the Partner WSDL and Enterprise WSDL version 40.0__

If you want build the OSGi bundle from the source code therefore required:
1. Sun/Oracle JDK 1.8
2. Maven 3.2
3. Git tools

### 1. How to use
If you need to access Salesforce via the SOAP APIs for your project development, then you could add to your project 
the dependency of the salesforce-client-soap bundle.

The last (release) version of the bundle is the [1.0.2](https://search.maven.org/#search%7Cga%7C1%7Cit.dontesta.labs.liferay.salesforce.client.soap) 
available on Maven Central Repository. Below the two dependencies, Gradle or Maven to add to your project.

```xml
<dependency>
	<groupId>it.dontesta.labs.liferay.salesforce.client.soap</groupId>
	<artifactId>salesforce-client-soap</artifactId>
	<version>1.0.2</version>
</dependency>
```
Code 1 - Maven dependency
```groovy
compile group:'it.dontesta.labs.liferay.salesforce.client.soap', name:'salesforce-client-soap', version:'1.0.2'
```
Code 2 - Gradle dependency

I implemented a series of [Gogo Shell commands](https://www.dontesta.it/en/liferay-7-salesforce-com-gogo-shell-command-client/) 
to interact with Salesforce using this OSGi bundle (salesforce-client-soap). The commands are:

1. **salesforce:login**: Login to your Salesforce instance
2. **salesforce:createAccount**: Create account into your Salesforce instance
3. **salesforce:getNewestAccount**: Query for the newest accounts
4. **salesforce:loginEnterprise**: Login to your Salesforce instance using the Enterprise Connection
5. **salesforce:getNewestAccountEnterprise**: Query for the newest accounts using the Enterprise Connection

The video is a demo of Gogo Shell commands that let you perform operations on Salesforge. _In this video not show the 
commands that use the Enterprise Connection._ 

[![Liferay 7: Demo Salesforce Gogo Shell Command ](https://img.youtube.com/vi/nQXqzKpnxoc/0.jpg)](https://youtu.be/nQXqzKpnxoc)

Video 1 - Liferay 7: Demo Salesforce Gogo Shell Command

### 2. How to install in Liferay 7 CE/DXP
For to install Salesforce SOAP API Client bundle in Liferay instance, we could proceed in two way:

1. Download the bundle JAR [salesforce-client-soap (v1.0.2)](http://repo1.maven.org/maven2/it/dontesta/labs/liferay/salesforce/client/soap/salesforce-client-soap/1.0.2/salesforce-client-soap-1.0.2.jar) 
from Maven repository and deploy to Liferay (via auto deploy directory or directly in *$LIFERAY_HOME/osgi/modules*);
2. Install via Gogo Shell (through install command)

```bash
$ telnel localhost 11311
g! install http://repo1.maven.org/maven2/it/dontesta/labs/liferay/salesforce/client/soap/salesforce-client-soap/1.0.2/salesforce-client-soap-1.0.2.jar
g! Bundle ID: 582
```
Console 1 - Install bundle via Gogo Shell

```bash
$ telenet localhost 11311
g! lb|grep Salesforce
  583|Active     |   10|Salesforce SOAP Client (1.0.2)
```
Console 2 - Verify the bundle just installed

### 3. How to install in Apache Karaf 4.x
As described earlier, this bundle can be installed on any [OSGi R6](https://www.osgi.org/developer/downloads/release-6/) 
compliant container, Apache Karaf is one of these containers. So let's see how to install the bundle.

```bash
karaf@root()> install http://repo1.maven.org/maven2/it/dontesta/labs/liferay/salesforce/client/soap/salesforce-client-soap/1.0.2/salesforce-client-soap-1.0.2.jar
Bundle ID: 52
karaf@root()> start 52
```
Console 3 - Install on Apache Karaf via Console

The bundle also can be installed by copying into *$KARAF_HOME/deploy* directory.

```bash
karaf@root()> list 52
START LEVEL 100 , List Threshold: 50
ID │ State  │ Lvl │ Version │ Name
───┼────────┼─────┼─────────┼──────────────────────────────────────────────────────────────────────────────────────────
52 │ Active │  80 │ 1.0.2   │ Salesforce SOAP Client
```
Console 4 - Verify the bundle just installed

### 4. Build OSGi bundle from source
If you want can build OSGi bundle from source in this way:

```bash
$ git clone https://github.com/amusarra/salesforce-client-soap.git
$ cd salesforce-client-soap/
$ mvn clean package
```
Console 5 - Clone & Build the OSGi bundle

Inside the target directory you will find the OSGi bundle JAR (for example: salesforce-client-soap-1.0.2-SNAPSHOT.jar).

### 5. Build OSGi bundle with its own Enterprise WSDL
If you want can build OSGi bundle with its own Enterprise WSDL then you proceed:

1. Generate the Enterprise Web Service WSDL for your organization and save locally (for example: enterprise_antonio_musarra_blog.wsdl).
To generate the WSDL file for your organization follow the guide [Generate or Obtain the Web Service WSDL](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_quickstart_steps_generate_wsdl.htm) 
2. Clone this repository
3. Build the source by specifying the location of the Enterprise WSDL (absolute path)

After getting your WSDL you can create your own OSGi bundle this way. Remember to replace 
```$YOUR_ABSOLUTE_PATH_ENTEPRISE_WSDL``` with the absolute path of the Enterprise WSDL.

```bash
$ git clone https://github.com/amusarra/salesforce-client-soap.git
$ cd salesforce-client-soap/
$ mvn -Dsalesforce.wsdl.enterprise.path=$YOUR_ABSOLUTE_PATH_ENTEPRISE_WSDL clean package
```

Inside the target directory you will find the OSGi bundle JAR (for example: salesforce-client-soap-1.0.3-SNAPSHOT.jar).
The following figure shows the content of the bundle showing the custom object of my Salesforce.com instance.

[![Salesforce SOAP API Client OSGi Bundle build from custom Enterprise WSDL](https://www.dontesta.it/wp-content/uploads/2017/08/SalesforceSOAPAPIClientOSGiBundleBuildFromCustomEnterpriseWSDL.png)](https://www.dontesta.it/wp-content/uploads/2017/08/SalesforceSOAPAPIClientOSGiBundleBuildFromCustomEnterpriseWSDL.png)

The figure below shows the use of the OSGi bundle just created as a dependency of another OSGi bundle 
[Salesforce Liferay Gogo Shell Command Client](https://www.dontesta.it/en/liferay-7-salesforce-com-gogo-shell-command-client/).

[![Salesforce Liferay Gogo Shell Command Client Usage Enterprise SObject](https://www.dontesta.it/wp-content/uploads/2017/08/SalesforceLiferayGogoShellCommandClientUsageEnterpriseSObject.png)](https://www.dontesta.it/wp-content/uploads/2017/08/SalesforceLiferayGogoShellCommandClientUsageEnterpriseSObject.png)


### 6. Resources
If you follow this resources you could see how to use Salesforce SOAP API.

1. [Introducing SOAP API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_quickstart_intro.htm)
2. [Force.com Web Service Connector (WSC)](https://github.com/forcedotcom/wsc)
3. [Salesforce Liferay Gogo Shell Command Client](https://www.dontesta.it/en/liferay-7-salesforce-com-gogo-shell-command-client/)

### Project License
The MIT License (MIT)

Copyright &copy; 2017 Antonio Musarra's Blog - [https://www.dontesta.it](https://www.dontesta.it "Antonio Musarra's Blog") , 
[antonio.musarra@gmail.com](mailto:antonio.musarra@gmail.com "Antonio Musarra Email")

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

<span style="color:#D83410">
	THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
	IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
	FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
	AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
	LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
	OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
	SOFTWARE.
<span>
