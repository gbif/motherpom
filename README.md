# motherpom
Base GBIF Maven pom to be used in all the GBIF Maven projects. Captures the common settings, plugins and profiles that
are shared by majority of GBIF projects. This pom artifact contains plugins to facilitate tasks like: generate
java-doc, deploy war file in web containers, publish java-doc sites, deploy artifacts in a Maven repository, 
run integration tests, execute unit tests, package jar files and execute database migrations using liquibase.

## How to use this artifact
In a Maven pom.xml file use it as the parent pom using the current version of this artifact:

```
<parent>
  <groupId>org.gbif</groupId>
  <artifactId>motherpom</artifactId>
  <version>XX</version>
</parent>
```
