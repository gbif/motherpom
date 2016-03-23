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
GitHub pages (used to display the JavaDocs on GitHub) are not generated automatically (see [Issue #1](https://github.com/gbif/motherpom/issues/1)).
This `motherpom` contains all the required plugins and configurations but in order to use it you need to add the following section to each projects where GitHub pages are needed:

```xml
  <distributionManagement>
    <site>
      <id>gh-pages</id>
      <url>http://gbif.github.io/${project.artifactId}/</url>
    </site>
  </distributionManagement>
```

**Multi-modules projects**
In the main pom:
```xml
  <url>http://gbif.github.io/${project.artifactId}/</url>
```
and this for the submodules:
```xml
  <url>http://gbif.github.io/${parent.artifactId}/${project.artifactId}/</url>
```

The following goals can then be included in the release command (e.g. Jenkins Maven Release plugin):
```
site site:stage scm-publish:publish-scm
```
