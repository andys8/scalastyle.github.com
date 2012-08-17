---
layout: scalastyle
title: "Scalastyle - Scala style checker"
---

Scalastyle examines your Scala code and indicates potential problems with it. If you have come across Checkstyle for Java,
then you'll have a good idea what scalastyle is. Except that it's for Scala obviously.

### How do I use scalastyle?

The latest stable version of Scalastyle is 0.1.0 for Scala 2.9.1. See the [Release Notes](release-notes.html)

There are several ways of using it:

 * [Maven Plugin](maven.html)
 * [Eclipse plugin (for 3.6 Helios)](eclipse-index.html)
 * [Command line](https://github.com/scalastyle/scalastyle-batch)

#### Download

To download Scalastyle, the jar is available from [Sonatype](https://oss.sonatype.org/content/repositories/releases/org/scalastyle/scalastyle_2.9.1).
<br/>
To scalastyle-batch (command line), this is also available from [Sonatype](https://oss.sonatype.org/content/repositories/releases/org/scalastyle/scalastyle-batch_2.9.1/). The latest version
of scalastyle-batch always contains the latest version of Scalastyle.
<br/>
For the maven plugin, see [Scalastyle Maven Plugin](maven.html)
<br/>
[Eclipse plugin (for 3.6 Helios)](eclipse-index.html): <br/>Stable update site (cut and paste into Eclipse)
<a href="http://www.scalastyle.org/downloads/helios/2.9.1-0.1.0/site">http://www.scalastyle.org/downloads/helios/2.9.1-0.1.0/site</a>

The latest development snapshots are available from [Sonatype snapshots](https://oss.sonatype.org/content/repositories/snapshots/org/scalastyle/)

### Rules

For a list of actual rules, see [Implemented Rules](rules-0.1.0.html).
For a list of (planned) rules, see the [Scalastyle WIKI](https://github.com/scalastyle/scalastyle/wiki).
If you want to add a rule, then please raise an [Issue](https://github.com/scalastyle/scalastyle/issues) (or even better a pull request)

For a list of rules in the latest development version, see [Development Implemented Rules](rules-dev.html).

### Questions and comments
If you have any questions, please see [Scalastyle users Google groups](https://groups.google.com/forum/#!forum/scalastyle-users)

### Github repositories

 * [Maven plugin](https://github.com/scalastyle/scalastyle-maven-plugin)
 * [Eclipse plugin](https://github.com/scalastyle/scalastyle-plugin)
 * [Command line](https://github.com/scalastyle/scalastyle-batch)

### Running scalastyle from the command line

This process will be improved in time, but for now, you need to build scalastyle and then build scalastyle-batch. First install scalastyle in your local maven repo

    $ git clone git://github.com/scalastyle/scalastyle.git
    $ cd scalastyle
    $ mvn install

Then get and build scalastyle-batch

    $ git clone git://github.com/scalastyle/scalastyle-batch.git
    $ cd scalastyle-batch
    $ mvn package # or mvn install

This will create in scalastyle-batch/target a zip file which contains an executable jar along with the dependencies in lib/. Unzip this file somewhere, and run the jar as such:

    $ java -jar scalastyle-batch_2.9.1.jar --config lib/scalastyle_config.xml src/main/scala

or similar. You can copy your initial configuration from lib/scalastyle_config.xml in the scalastyle project, and change it from there.

### Maven repo

Snapshots are available from the Sonatype nexus repository: https://oss.sonatype.org/content/repositories/snapshots/.
To use, add something like the following to your settings.xml:

    <repository>
      <id>sonatype-nexus-snapshots</id>
      <name>Sonatype OSS</name>
      <url>https://oss.sonatype.org/content/repositories/releases/</url>
      <layout>default</layout>
      <releases>
        <enabled>true</enabled>
        <updatePolicy>never</updatePolicy>
      </releases>
      <snapshots>
        <enabled>false</enabled>
        <updatePolicy>never</updatePolicy>
      </snapshots>
    </repository>

There are only snapshots available at the minute.

### Testing

To run the tests:

    $ mvn test

### Contributing

Want to contribute? Great! Look at the wiki for potential rules to implement, or do one of your own, and implement it.

1. Read the [developer guide](developer-guide.html)
2. Fork the repo.
3. Create a branch (`git checkout -b my_new_rule`)
4. Commit your changes (`git commit -am "Added NoFooAllowed"`)
5. Push to the branch (`git push origin my_new_rule`)
6. Create an [Issue](https://github.com/scalastyle/scalastyle/issues) with a link to your branch
7. Enjoy a coffee and wait

### Comment filters

If you wish to ignore a particular scalastyle rule, you can put a comment before and after the line, with the following syntax:

    // scalastyle:off
    // scalastyle:on

You can also switch off checking for a particular rule by specifying the id of the rule to ignore:

    // scalastyle:off magic.number
    var foobar = 134
    // scalastyle:on magic.number

### Custom messages

Messages are defined within the scalastyle_messages.properties. If however, you wish to have a custom error message for a particular rule, then
you can do so by defining a customMessage element in the configuration, such as:

    <check level="warning" class="org.scalastyle.scalariform.MagicNumberChecker" enabled="true">
     <customMessage>Please don't use magic numbers</customMessage>
    </check>