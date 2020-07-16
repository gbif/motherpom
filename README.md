# GBIF Motherpom
Base GBIF Maven POM to be used in all the GBIF Maven projects. Captures the common settings, plugins and profiles that
are shared by majority of GBIF projects. This POM artifact contains plugins to facilitate tasks like: generate
java-doc, publish java-doc sites, deploy artifacts in a Maven repository,
run integration tests, execute unit tests, package JAR files and execute database migrations using Liquibase and so on.


## How to use this artifact
In a Maven pom.xml file use it as the parent POM using the current version of this artifact:

```
<parent>
  <groupId>org.gbif</groupId>
  <artifactId>motherpom</artifactId>
  <version>XX</version>
</parent>
```

## Override properties

Some properties should be overridden in child projects.

- main.basedir — This property should provide the path of the project root. In the child project's root POM:

```xml
  <properties>
    <main.basedir>${project.basedir}</main.basedir>
  </properties>
```

In a child project's submodule POM:

```xml
  <properties>
    <main.basedir>${project.parent.basedir}</main.basedir>
  </properties>
```

In a subsubmodule:

```xml
  <properties>
    <main.basedir>${project.parent.parent.basedir}</main.basedir>
  </properties>
```
and so on. These properties help to get files with an import order configuration and a license header.

## Configure a project to use motherpom

This project uses spotless-maven-plugin and requires some configuration files. These files should be present in the root of child project (**configuration is for Intellij IDEA 2019.3.2 and it may differ in a later versions**):

- [gbif.importorder](./gbif.importorder) overrides default google package import order (for spotless-maven-plugin).
- [gbif-lecense-header](./gbif-license-header) provides default license header (for spotless-maven-plugin).
- [google-style.xml](./google-style.xml) Java Google code style, should be imported to IDE as a default one: Preferences → Editor → Code Style → Import scheme (gear next to 'Scheme' dropdown) → Intellij IDEA code style XML.
- [.editorconfig](./.editorconfig) formatting properties which overrides some inconvenient Google ones (e.g. static imports at the beginning of imports list). Make sure editorconfig file is enabled in IDE: Preferences → Editor → Code Style → General → Enable EditorConfig support.

## Manual use of Spotless

Check that project follows code style conventions:

```
mvn spotless:check
```

Fix code style violations:

```
mvn spotless:apply
```

For more information see the [documentation](https://github.com/diffplug/spotless/tree/master/plugin-maven).

## GitHub Pages
GitHub pages (used to display the JavaDocs on GitHub) are not generated automatically (see [Issue #1](https://github.com/gbif/motherpom/issues/1)).
This `motherpom` contains all the required plugins and configurations but in order to use it you need to add the following section to each projects where GitHub pages are needed:

```xml
  <distributionManagement>
    <site>
      <id>gh-pages</id>
      <url>https://gbif.github.io/${project.artifactId}/</url>
    </site>
  </distributionManagement>
```

## Notes
The following goals can then be included in the release command (e.g. Jenkins Maven Release plugin):
```
site site:stage scm-publish:publish-scm
```

It is possible to use the variable `${project.artifactId}` even if the project is stored on GitHub under another name.

> On the other hand, the `<distributionManagement.url>` is used in a multi-module build to construct relative links between the generated sub-module sites. In a multi module build it is important for the parent and child modules to have different URLs. If they have the same URL, then links within the combined site will not work. Note that a proper URL should also be terminated by a slash ("/").

Source: http://maven.apache.org/plugins/maven-site-plugin/faq.html#Use_of_url
