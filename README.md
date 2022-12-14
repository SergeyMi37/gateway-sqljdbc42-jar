[![Repo-GitHub](https://img.shields.io/badge/dynamic/xml?color=gold&label=GitHub%20module.xml&prefix=ver.&query=%2F%2FVersion&url=https%3A%2F%2Fraw.githubusercontent.com%2Fsergeymi37%2Fgateway-sqljdbc42-jar/%2Fmaster%2Fmodule.xml)](https://raw.githubusercontent.com/sergeymi37/gateway-sqljdbc42-jar/master/module.xml)
 
![OEX-zapm](https://img.shields.io/badge/dynamic/json?url=https:%2F%2Fpm.community.intersystems.com%2Fpackages%2Fgateway-sqljdbc42-jar%2F&label=ZPM-pm.community.intersystems.com&query=$.version&color=green&prefix=gateway-sqljdbc42-jar)
 
[![Docker-ports](https://img.shields.io/badge/dynamic/yaml?color=blue&label=docker-compose&prefix=ports%20-%20&query=%24.services.iris.ports&url=https%3A%2F%2Fraw.githubusercontent.com%2Fsergeymi37%2Fgateway-sqljdbc42-jar%2Fmaster%2Fdocker-compose.yml)](https://raw.githubusercontent.com/sergeymi37/gateway-sqljdbc42-jar/master/docker-compose.yml)
 
## gateway-sqljdbc42-jar
Module for importing instances of the %Library.SQLConnection class into the %SYS namespace, copying the jdbс driver `sqljdbc42.jar`.

## Installation with ZPM

If ZPM the current instance is not installed, then in one line you can install the latest version of ZPM.
```
set $namespace="%SYS", name="DefaultSSL" do:'##class(Security.SSLConfigs).Exists(name) ##class(Security.SSLConfigs).Create(name) set url="https://pm.community.intersystems.com/packages/zpm/latest/installer" Do ##class(%Net.URLParser).Parse(url,.comp) set ht = ##class(%Net.HttpRequest).%New(), ht.Server = comp("host"), ht.Port = 443, ht.Https=1, ht.SSLConfiguration=name, st=ht.Get(comp("path")) quit:'st $System.Status.GetErrorText(st) set xml=##class(%File).TempFilename("xml"), tFile = ##class(%Stream.FileBinary).%New(), tFile.Filename = xml do tFile.CopyFromAndSave(ht.HttpResponse.Data) do ht.%Close(), $system.OBJ.Load(xml,"ck") do ##class(%File).Delete(xml)
```
If ZPM is installed, then `gateway-sqljdbc42-jar` can be set with the command
```
zpm:%SYS>install gateway-sqljdbc42-jar
```
## Installation with Docker

## Prerequisites
Make sure you have [git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) and [Docker desktop](https://www.docker.com/products/docker-desktop) installed.

## Installation
Clone/git pull the repo into any local directory

```
$ git clone https://github.com/SergeyMi37/gateway-sqljdbc42-jar
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
...
```

You can import a class %Library.SQLConnection instance in the %SYS namespace with the command:

```
%SYS>do ##class(appmsw.gateway.jdbc).ImportSQLConnection()
...

saved

```
