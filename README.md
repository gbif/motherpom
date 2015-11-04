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

## GitHub Pages
The `gh-pages` profile will be activated and will run as part of the `release:perform` goal.
It is configured with the following:
```xml
<plugin>
...
  <artifactId>maven-release-plugin</artifactId>
  <configuration>
    <goals>deploy site-deploy</goals>
...
    <releaseProfiles>gbif-release,gh-pages</releaseProfiles>
...
```
