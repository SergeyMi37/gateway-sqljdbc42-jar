[![Repo-GitHub](https://img.shields.io/badge/dynamic/xml?color=gold&label=GitHub%20module.xml&prefix=ver.&query=%2F%2FVersion&url=https%3A%2F%2Fraw.githubusercontent.com%2Fsergeymi37%2Fgateway-mysql-connector-java-8-0-21-jar%2Fmaster%2Fmodule.xml)](https://raw.githubusercontent.com/sergeymi37/gateway-mysql-connector-java-8-0-21-jar/master/module.xml)
 
![OEX-zapm](https://img.shields.io/badge/dynamic/json?url=https:%2F%2Fpm.community.intersystems.com%2Fpackages%2Fgateway-mysql-connector-java-8-0-21-jar%2F&label=ZPM-pm.community.intersystems.com&query=$.version&color=green&prefix=gateway-mysql-connector-java-8-0-21-jar)
 
[![Docker-ports](https://img.shields.io/badge/dynamic/yaml?color=blue&label=docker-compose&prefix=ports%20-%20&query=%24.services.iris.ports&url=https%3A%2F%2Fraw.githubusercontent.com%2Fsergeymi37%2Fgateway-mysql-connector-java-8-0-21-jar%2Fmaster%2Fdocker-compose.yml)](https://raw.githubusercontent.com/sergeymi37/gateway-mysql-connector-java-8-0-21-jar/master/docker-compose.yml)
 
## gateway-mysql-connector-java-8-0-21-jar

## What's new

Module for importing instances of the %Library.SQLConnection class into the %SYS namespace, copying the jdbс driver `mysql-connector-java-8.0.21.jar`.

## Installation with ZPM

If ZPM the current instance is not installed, then in one line you can install the latest version of ZPM.
```
set $namespace="%SYS", name="DefaultSSL" do:'##class(Security.SSLConfigs).Exists(name) ##class(Security.SSLConfigs).Create(name) set url="https://pm.community.intersystems.com/packages/zpm/latest/installer" Do ##class(%Net.URLParser).Parse(url,.comp) set ht = ##class(%Net.HttpRequest).%New(), ht.Server = comp("host"), ht.Port = 443, ht.Https=1, ht.SSLConfiguration=name, st=ht.Get(comp("path")) quit:'st $System.Status.GetErrorText(st) set xml=##class(%File).TempFilename("xml"), tFile = ##class(%Stream.FileBinary).%New(), tFile.Filename = xml do tFile.CopyFromAndSave(ht.HttpResponse.Data) do ht.%Close(), $system.OBJ.Load(xml,"ck") do ##class(%File).Delete(xml)
```
If ZPM is installed, then `gateway-mysql-connector-java-8-0-21-jar` can be set with the command
```
zpm:%SYS>install gateway-mysql-connector-java-8-0-21-jar
```
## Installation with Docker

## Prerequisites
Make sure you have [git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) and [Docker desktop](https://www.docker.com/products/docker-desktop) installed.

## Installation
Clone/git pull the repo into any local directory

```
$ git clone https://github.com/SergeyMi37/gateway-mysql-connector-java-8-0-21-jar
```

Open the terminal in this directory and run:

```
$ docker-compose build
```

3. Run the IRIS container with your project:

```
$ docker-compose up -d

$ docker-compose exec iris iris session iris
```

## How to Test it

You can see what instances of the %Library.SQLConnection class are in the module by running a command in the %SYS namespace:

```
%SYS>do ##class(appmsw.gateway.jdbc).ImportSQLConnection("view")

%Library.SQLConnection. DSN =  type:string
%Library.SQLConnection. Name = Default_Name_SQLConnection type:string
%Library.SQLConnection. OnConnectStatement =  type:string
%Library.SQLConnection. ReverseOJ = 0 type:number
%Library.SQLConnection. URL = jdbc:mysql://ip address:port/databaseName?serverTimezone=UTC type:string
%Library.SQLConnection. Usr = Default_DB_UserName type:string
%Library.SQLConnection. bUnicodeStream = 0 type:number
%Library.SQLConnection. bindTSasString = 0 type:number
%Library.SQLConnection. classpath = /opt/oracle/mysql-connector-java-8.0.21.jar type:string
%Library.SQLConnection. driver =  type:string
%Library.SQLConnection. isJDBC =  type:string
%Library.SQLConnection. needlongdatalen =  type:string
%Library.SQLConnection. noconcat =  type:string
%Library.SQLConnection. nodefq =  type:string
%Library.SQLConnection. nofnconv =  type:string
%Library.SQLConnection. nvl =  type:string
%Library.SQLConnection. properties =  type:string
%Library.SQLConnection. pwd =  type:string
%Library.SQLConnection. useCAST =  type:string
%Library.SQLConnection. useCASTCHAR =  type:string
%Library.SQLConnection. useCOALESCE = 1 type:number
%Library.SQLConnection. xadriver =  type:string

```

You can import a class %Library.SQLConnection instance in the %SYS namespace with the command:

```
%SYS>do ##class(appmsw.gateway.jdbc).ImportSQLConnection()

Change the value of a field 'Name' <Default_Name_SQLConnection> test2
Change the value of a field 'URL' <jdbc:mysql://ip address:port/databaseName?serverTimezone=UTC>
Change the value of a field 'Usr' <Default_DB_UserName>
Change the value of a field 'classpath' </opt/oracle/mysql-connector-java-8.0.21.jar> /opt/irisbuild/mysql-connector-java-8.0.21.jar
Copied from /usr/irissys/lib/jdbc/mysql-connector-java-8.0.21.jar to /opt/irisbuild/mysql-connector-java-8.0.21.jar
Change the value of a field 'driver' <>
The password will need to be entered in the portal interface

saved

```
