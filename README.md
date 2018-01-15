Build Resources
===============

<a href="https://raw.githubusercontent.com/InscopeMetrics/build-resources/master/LICENSE">
    <img src="https://img.shields.io/hexpm/l/plug.svg"
         alt="License: Apache 2">
</a>
<a href="https://travis-ci.org/InscopeMetrics/build-resources/">
    <img src="https://travis-ci.org/InscopeMetrics/build-resources.png?branch=master"
         alt="Travis Build">
</a>
<a href="http://search.maven.org/#search%7Cga%7C1%7Cg%3A%22com.inscopemetrics.build%22%20a%3A%22build-resources%22">
    <img src="https://img.shields.io/maven-central/v/com.inscopemetrics.build/build-resources.svg"
         alt="Maven Artifact">
</a>

Resources for building Inscope Metrics projects.

Usage
-----

### Appassembler

The recommended way to consume the Appassembler resource is through the [Inscope Metrics Parent Pom](https://github.com/InscopeMetrics/parent-pom). However, manual
configuration is pretty straight-forward; after exploding the contents of the build-resources artifact simply configure Appassembler like this:

```xml
<configuration>
  <unixScriptTemplate>${project.basedir}/target/build-resources/unixBinTemplate</unixScriptTemplate>
</configuration>
```

### Checkstyle / Findbugs

The recommended way to consume the Checkstyle and Findbugs resources is through the [Inscope Metrics Parent Pom](https://github.com/InscopeMetrics/parent-pom).
Nevertheless, it is possible to use these build resources without using the parent-pom or even without using Maven. However, this is not trivial and is therefore
not documented here and not recommended.

### IntelliJ

If your project uses the [Inscope Metrics Parent Pom](https://github.com/InscopeMetrics/parent-pom) then the build-resources are extracted
into your _target/build-resources_ directory by default. You can import the IntelliJ configuration from there or download it from this
repository.

To add code style configuration:
* Open IntelliJ Preferences
* Browse to: Editor / Code Style / Java
* Click the gear drop down button near the top
* Select the "Import Scheme" option
* Locate the file _target/build-resources/intellij-code-style.xml_

To add inspections configuration:
* Open IntelliJ Preferences
* Browse to: Editor / Inspections
* Click the gear drop down button near the top
* Select the "Import Scheme" option
* Locate the file _target/build-resources/intellij-inspections.xml_

Building
--------

This project uses the [Inscope Metrics Parent Pom](https://github.com/InscopeMetrics/parent-pom) with the
[JDK Wrapper](https://github.com/vjkoskela/jdk-wrapper) and the [Maven Wrapper](https://github.com/rimerosolutions/maven-wrapper) enabled.
While you can conjure up the correct build command, the [Inscope Metrics Parent Pom](https://github.com/InscopeMetrics/parent-pom) includes
a simple script to detect the appropriate build tools and invoke them for you.

Prerequisites:
* [JDK8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) (Or Invoke with [JDK Wrapper](https://github.com/vjkoskela/jdk-wrapper))

Building:

```
> mvn verify
```

To use the local version you must first install it locally:

```
> mvn install
```

You can determine the version of the local build from the pom file.  Using the local version is intended only for testing or development.

Releasing
---------

This project is versioned using [semantic versioning](http://semver.org/) please consult the commit history to determine
the next appropriate release version. Next, simply invoke the Maven Release plugin which will interactively query for the
version of the artifact to release:

```
> mvn release:prepare && mvn release:clean && git pull
```

The plugin will update the version and SCM tag in _pom.xml_ automatically based on your input and then commit the changes
to source control. When releasing the build system (e.g. [Travis](travis-ci.org)) must execute the _deploy_ lifecycle,
enable the _release_ profile, and provide the _settings.xml_ file:

```
> mvn deploy -P release --settings settings.xml
```

License
-------

Published under Apache Software License 2.0, see LICENSE

&copy; Inscope Metrics Incorporated, 2018
