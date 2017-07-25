
# Salesforce SOAP API Client Bundle
This project implements an OSGi bundle to interact with Salesforge SOAP APIs. The OSGi bundle is created through the **Force.com Web Service Connector (WSC) version 40.1.1** and export this package:

1. com.sforce.soap.partner.*
2. com.sforce.ws.*

### 1. How to use
If you need to access Salesforce via the SOAP APIs for your project development, then you could add to your project the dependency of the salesforce-client-soap bundle.

The last version of the bundle is the [1.0.0](https://search.maven.org/#search%7Cga%7C1%7Cit.dontesta.labs.liferay.salesforce.client.soap) available on Maven Central Repository. Below the two dependencies, Gradle or Maven to add to your project.

```xml
<dependency>
	<groupId>it.dontesta.labs.liferay.salesforce.client.soap</groupId>
	<artifactId>salesforce-client-soap</artifactId>
	<version>1.0.0</version>
</dependency>
```
Code 1 - Maven dependency
```
compile group:'it.dontesta.labs.liferay.salesforce.client.soap', name:'salesforce-client-soap', version:'1.0.0'
```
Code 2 - Gradle dependency

### 2. How to install in Liferay 7 CE/DXP
For to install Salesforce SOAP API Client bundle in Liferay instance, we could proceed in two way:

1. Download the bundle JAR [salesforce-client-soap (v1.0.0)](http://repo1.maven.org/maven2/it/dontesta/labs/liferay/salesforce/client/soap/salesforce-client-soap/1.0.0/salesforce-client-soap-1.0.0.jar) from Maven repository and deploy to Liferay (via auto deploy directory or directly in $LIFERAY_HOME/osgi/modules);
2. Install via Gogo Shell (through install command)

```c
$ telnel localhost 11311
g! install http://repo1.maven.org/maven2/it/dontesta/labs/liferay/salesforce/client/soap/salesforce-client-soap/1.0.0/salesforce-client-soap-1.0.0.jar
g! Bundle ID: 582
```
Console 1 - Install bundle via Gogo Shell

```c
$ telenet localhost 11311
g! lb|grep Salesforce
  583|Active     |   10|Salesforce SOAP Client (1.0.0)
```
Console 2 - Verify the bundle just installed

### 3. Resources
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
