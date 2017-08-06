
# Salesforce SOAP API Client OSGi Bundle
[![Build Status](https://travis-ci.org/amusarra/salesforce-client-soap.svg?branch=master)](https://travis-ci.org/amusarra/salesforce-client-soap)
[![Maven Central](https://maven-badges.herokuapp.com/maven-central/it.dontesta.labs.liferay.salesforce.client.soap/salesforce-client-soap/badge.svg)](https://search.maven.org/#artifactdetails%7Cit.dontesta.labs.liferay.salesforce.client.soap%7Csalesforce-client-soap%7C1.0.2%7Cjar)
[![](https://img.shields.io/badge/download-OSGi%20Bundle-green.svg)](http://repo1.maven.org/maven2/it/dontesta/labs/liferay/salesforce/client/soap/salesforce-client-soap/1.0.1/salesforce-client-soap-1.0.2.jar)

[![Twitter URL](https://img.shields.io/twitter/url/http/shields.io.svg?style=social)](https://twitter.com/antonio_musarra)

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

This Salesforce SOAP API Client Bundle use the Partner WSDL and Enterprise WSDL version 40.0

If you want build the OSGi bundle from the source code therefore required:
1. Sun/Oracle JDK 1.8
2. Maven 3.2
3. Git tools

### 1. How to use
If you need to access Salesforce via the SOAP APIs for your project development, then you could add to your project the dependency of the salesforce-client-soap bundle.

The last version of the bundle is the [1.0.2](https://search.maven.org/#search%7Cga%7C1%7Cit.dontesta.labs.liferay.salesforce.client.soap) available on Maven Central Repository. Below the two dependencies, Gradle or Maven to add to your project.

```xml
<dependency>
	<groupId>it.dontesta.labs.liferay.salesforce.client.soap</groupId>
	<artifactId>salesforce-client-soap</artifactId>
	<version>1.0.2</version>
</dependency>
```
Code 1 - Maven dependency
```
compile group:'it.dontesta.labs.liferay.salesforce.client.soap', name:'salesforce-client-soap', version:'1.0.2'
```
Code 2 - Gradle dependency

Using this OSGi bundle, I implemented a series of Gogo Shell commands to interact with Salesforce. The commands are:

1. **salesforce:login**: Login to your Salesforce instance
2. **salesforce:createAccount**: Create account into your Salesforce instance
3. **salesforce:getNewestAccount**: Query for the newest accounts

The video is a demo of Gogo Shell commands that let you perform operations on Salesforge.

[![Liferay 7: Demo Salesforce Gogo Shell Command ](https://img.youtube.com/vi/nQXqzKpnxoc/0.jpg)](https://youtu.be/nQXqzKpnxoc)

Video 1 - Liferay 7: Demo Salesforce Gogo Shell Command

### 2. How to install in Liferay 7 CE/DXP
For to install Salesforce SOAP API Client bundle in Liferay instance, we could proceed in two way:

1. Download the bundle JAR [salesforce-client-soap (v1.0.1)](http://repo1.maven.org/maven2/it/dontesta/labs/liferay/salesforce/client/soap/salesforce-client-soap/1.0.1/salesforce-client-soap-1.0.1.jar) from Maven repository and deploy to Liferay (via auto deploy directory or directly in *$LIFERAY_HOME/osgi/modules*);
2. Install via Gogo Shell (through install command)

```sh
$ telnel localhost 11311
g! install http://repo1.maven.org/maven2/it/dontesta/labs/liferay/salesforce/client/soap/salesforce-client-soap/1.0.1/salesforce-client-soap-1.0.1.jar
g! Bundle ID: 582
```
Console 1 - Install bundle via Gogo Shell

```sh
$ telenet localhost 11311
g! lb|grep Salesforce
  583|Active     |   10|Salesforce SOAP Client (1.0.1)
```
Console 2 - Verify the bundle just installed

### 3. How to install in Apache Karaf 4.x
As described earlier, this bundle can be installed on any [OSGi R6](https://www.osgi.org/developer/downloads/release-6/) compliant container, Apache Karaf is one of these containers. So let's see how to install the bundle.

```sh
karaf@root()> install http://repo1.maven.org/maven2/it/dontesta/labs/liferay/salesforce/client/soap/salesforce-client-soap/1.0.1/salesforce-client-soap-1.0.1.jar
Bundle ID: 52
karaf@root()> start 52
```
Console 3 - Install on Apache Karaf via Console

The bundle also can be installed by copying into *$KARAF_HOME/deploy* directory.

```sh
karaf@root()> list 52
START LEVEL 100 , List Threshold: 50
ID │ State  │ Lvl │ Version │ Name
───┼────────┼─────┼─────────┼──────────────────────────────────────────────────────────────────────────────────────────
52 │ Active │  80 │ 1.0.1   │ Salesforce SOAP Client
```
Console 4 - Verify the bundle just installed

### 4. Build bundle from source
If you want can build OSGi bundle from source in this way:

```sh
$ git clone https://github.com/amusarra/salesforce-client-soap.git
$ cd salesforce-client-soap/
$ mvn clean package
```
Console 5 - Clone & Build the OSGi bundle

Inside the target directory you will find del OSGi bundle JAR (for example: salesforce-client-soap-1.0.2-SNAPSHOT.jar).

### 5. Resources
If you follow this resources you could see how to use Salesforce SOAP API.

1. [Introducing SOAP API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_quickstart_intro.htm)
2. [Force.com Web Service Connector (WSC)](https://github.com/forcedotcom/wsc)

### Project License
The MIT License (MIT)

Copyright &copy; 2017 Antonio Musarra's Blog - [https://www.dontesta.it](https://www.dontesta.it "Antonio Musarra's Blog") , [antonio.musarra@gmail.com](mailto:antonio.musarra@gmail.com "Antonio Musarra Email")

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
