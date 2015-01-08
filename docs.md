---
layout: page
title: Documentation
permalink: /docs/
---


### Downloading

Get Tarql latest releases from the [dowloads page](http://lab.linkeddata.deri.ie/2013/tarql/) of the project. This documentation is for Tarql version 10a.
The downloads page contains Tarql versions with all dependencies. 

Tarql runs on both Windows and Unix systems. It runs locally in a single machine --- all you need is to have `java` version 1.7 or above installed on your system, 
and configure `PATH`, or the `JAVA_HOME` environment variables pointing to the Java installation.

### Building from Source Code

Get the code from [Tarql GitHub Project](http://github.com/cygri/tarql)

Tarql uses Maven. To create executable scripts for Windows and Unix in `/target/appassembler/bin/`:

{% highlight bash %}
    ~$ mvn clean install -DskipTests
{% endhighlight %}

### Running the Examples

To run the examples you need to first create the executable scripts as explained in last point.

{% highlight bash %}
	~$ cd tarql/target/appassembler
	~$ sh bin/tarql --ntriples ../../examples/sample-2.sparql ../../examples/TechCrunchcontinentalUSA.csv
{% endhighlight %}

### Documentation

Java documentation is available [here](/tarql/docs/index.html).

### Community

_TBC: mailing list_

#### Reporting Issues

If you'd like to report a bug in Tarql or ask for a new feature, open an issue on the [Tarql GitHub Project](https://github.com/cygri/tarql/issues). For general usage help, you should email the user [mailing list]().

#### Contribute Code

You can contribute to the project submitting GitHub pull requests. Start by opening an issue for your change on the [Tarql GitHub Project](https://github.com/cygri/tarql/issues) (and make sure to search whether
there is an existing issue). Please use descriptive names in your pull requests. You can always check the code in the [https://github.com/cygri/tarql] repository.
