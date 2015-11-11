Setting up your development environment
===
This chapter describes how to build your first application using
Apache Apex and Malhar. Internet connectivity will be required for some of the
steps in this chapter since we will download code from the Apache Apex and
Malhar repositories.

Prerequisites
---
To build applications using Apex and Malhar, you must have:

-   JAVA Development KIT (JDK) version 1.7.0\_79 or later
-   Apache Maven version 3.0.5 or later
-   Git version 1.9.1 or later

To ensure that you have the correct version, shown below:

<table>
<colgroup>
<col width="20%" />
<col width="80%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Command</p></td>
<td align="left"><p>Expected output</p></td>
</tr>
<tr class="even">
<td align="left"><p><b>java -version</b></p></td>
<td align="left"><p>java version &quot;1.7.0_79&quot;</p>
<p>Java(TM) SE Runtime Environment (build 1.7.0_79-b15)</p>
<p>Java HotSpot(TM) 64-Bit Server VM (build 24.79-b02, mixed mode)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><b>mvn --version</b></p></td>
<td align="left"><p>Apache Maven 3.0.5</p>
<p>Maven home: /usr/share/maven</p>
<p>Java version: 1.7.0_79, vendor: Oracle Corporation</p>
<p>Java home: /home/&lt;user&gt;/Software/java/jdk1.7.0_79/jre</p>
<p>Default locale: en_US, platform encoding: UTF-8</p>
<p>OS name: &quot;linux&quot;, version: &quot;3.16.0-44-generic&quot;, arch: &quot;amd64&quot;, family: &quot;unix&quot;</p></td>
</tr>
<tr class="even">
<td align="left"><p><b>git --version</b></p></td>
<td align="left"><p>git version 1.9.1</p></td>
</tr>
</tbody>
</table>

Download and install Apache Apex Core and Malhar
---
To download Apache Apex core and malhar

1.  Create a new directory where you want the code to reside and step into it:

    `cd ~/src; mkdir dt; cd dt`

2.  From this newly-created directory, run the following commands to download
    Apex and Malhar using Git (more about the git clone
    command [here](http://git-scm.com/docs/git-clone))

        git clone https://github.com/apache/incubator-apex-core
        git clone https://github.com/apache/incubator-apex-malhar

    These commands will create directories `incubator-apex-core` and
    `incubator-apex-malhar`

3.  Run the following commands to build apex-core:

        pushd incubator-apex-core
        git checkout release-3.1
        mvn clean install -DskipTests
        popd

4.  Run the following commands to build apex-malhar:

        pushd incubator-apex-malhar
        git checkout release-3.1
        mvn clean install -DskipTests
        popd

_Note_: The install argument to the `mvn` command installs resources
from each project to your local maven repository (typically
`~/.m2/repository`), and NOT the system directories so you do not need
root (i.e.  super-user) privileges to run these commands. We use the
`-DskipTests` argument to skip running unit tests since they take a long
time.

When this guide was written, 3.1 was the latest release; if a
later release is available, use the appropriate branch for that
release, for example `release-3.2`.

If this is a first-time installation, it might take longer to
complete because a Maven installation also includes download of
associated plugins.

Run pre-built applications
---

Malhar comes with pre-built applications, each in its own subdirectory
under `incubator-apex-malhar/demos`. Some of these applications are
standalone in nature, while some require external data resources, for
example, Twitter demo requires a Twitter feed. The build creates an
application package, or an `.apa` file for each application in the
target subdirectory, and each such package might contain multiple
applications.

Here is a summary of the pre-built applications under the `demos` directory.

<table>
<colgroup>
<col width="20%" />
<col width="80%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Application</p></td>
<td align="left"><p>Description</p></td>
</tr>
<tr class="even">
<td align="left"><p>echoserver</p></td>
<td align="left"><p>Reads messages from a network connection and echoes them.</p></td>
</tr>
<tr class="odd">
<td align="left"><p>frauddetect</p></td>
<td align="left"><p>Analyzes a stream of credit card merchant transactions.</p></td>
</tr>
<tr class="even">
<td align="left"><p>machinedata</p></td>
<td align="left"><p>Analyzes a synthetic stream of events to determine the health of a machine.</p></td>
</tr>
<tr class="odd">
<td align="left"><p>mobile</p></td>
<td align="left"><p>Demonstrates scalability of the DataTorrent platform by analyzing a synthetic stream of location data for a large number of cell phone connections.</p></td>
</tr>
<tr class="even">
<td align="left"><p>mroperator</p></td>
<td align="left"><p>Contains MapReduce applications.</p></td>
</tr>
<tr class="odd">
<td align="left"><p>pi</p></td>
<td align="left"><p>Computes the value of pi (&pi;) using the Monte Carlo method.</p></td>
</tr>
<tr class="even">
<td align="left"><p>r</p></td>
<td align="left"><p>Analyzes a synthetic stream of eruption event data for the Old Faithful geyser (<a href="https://en.wikipedia.org/wiki/Old_Faithful">Old_Faithful</a>). </p></td>
</tr>
<tr class="odd">
<td align="left"><p>twitter</p></td>
<td align="left"><p>Analyzes live tweet data from a Twitter stream for a Twitter account. </p></td>
</tr>
<tr class="even">
<td align="left"><p>yahoofinance</p></td>
<td align="left"><p>Analyzes live stock transaction data.</p></td>
</tr>
</tbody>
</table>

To run pre-built applications we use the commandline tool `dtcli`:

1.  Define a convenient alias and run the `dtcli` command, for example:

        cd ~
        alias dtcli=`pwd`/incubator-apex-core/engine/src/main/scripts/dtcli
        dtcli

    It may display a warning about the stack guard being disabled
    in `libhadoop.so`; the warning can be ignored.

2.  At the `dt>` prompt, type `help` to see a list of available commands and a
    brief description for each. To exit the application, press CTRL-D or type `exit`.
    The left/right arrow keys will move the cursor and the up/down arrow keys
    will scan through command history just like a shell. Now, define these variables
    for convenience:

        wc=incubator-apex-malhar/demos/wordcount/target/wordcount-demo-3.1.0-SNAPSHOT.apa
        uc=incubator-apex-malhar/demos/uniquecounttarget/uniquecount-3.1.0-SNAPSHOT.apa

3.  Run the standalone applications using these commands (you can press CTRL-C
    to exit the application and return to the prompt):

<table>
<colgroup>
<col width="25%" />
<col width="75%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Command</p></td>
<td align="left"><p>Description</p></td>
</tr>
<tr class="even">
<td align="left"><p><b>launch --local $wc</b></p></td>
<td align="left"><p>Displays a list of unique words encountered in each window of the input stream along with a frequency count for each. The input for this application comes from the file `demos/wordcount/src/main/resources/samplefile.txt`</p></td>
</tr>
<tr class="odd">
<td align="left"><p><b>launch --local $uc</b></p></td>
<td align="left"><p>Displays the list of two applications present in this jar. Choose  1 , which corresponds to the application named <b>UniqueKeyValueCountDemo</b>. It should displays the unique key-value pairs and a frequency count for each. The input for this application is randomly generated.</p></td>
</tr>
</tbody>
</table>

_Note_: The `--local` option runs the application in local mode, without a cluster.
Running it in a Hadoop cluster is an advanced feature that we will cover later.

Build your first application
---
This section describes how you can build an application from
scratch. This example application creates an unending sequence of random
numbers and prints them with the `hello world:` prefix, for example:
`hello world: 0.30266721560549`

The application comprises two source files: `Application.java` and
`RandomNumberGenerator.java`.  The former contains the application
code that instantiates operators and connects them to form a Directed
Acyclic Graph (DAG). The latter is an operator that generates a
sequence of random numbers. The DAG uses a second operator,
`ConsoleOutputOperator`, which prints input tuples to the console.
The source file for this operator is in the Malhar library.

To build an application

1.  Open a file in a simple text editor.
2.  Copy the following script to this file.

        #!/bin/bash
        # Script for creating a new application
        mvn archetype:generate \
        -DarchetypeRepository=https://www.datatorrent.com/maven/content/repositories/releases \
          -DarchetypeGroupId=com.datatorrent \
          -DarchetypeArtifactId=apex-app-archetype \
          -DarchetypeVersion=3.1.1 \
          -DgroupId=com.example \
          -Dpackage=com.example.myapexapp \
          -DartifactId=myapexapp \
          -Dversion=1.0-SNAPSHOT

3.  Save the file as, for example, `newdt.sh`.

4.  Run the file using the following command to generate a new Maven project:

        bash Name_of_the_file.sh

    For example, the command might look like this: `bash newdt.sh`
    _Note_: The command details are based on the contents of
    `incubator-apex-core/apex-app-archetype/README.md` and might require adjustments
    for newer versions of Apex. The command properties are displayed when you
    run this command.

5.  At the prompt, press _Enter_ to create a new project in a directory named
    `myapexapp`.

6.  From the new directory, run the maven command to build the project:

        cd myapexapp
        mvn clean package -DskipTests

The build should create the `myapexapp/target/myapexapp-1.0-SNAPSHOT.apa` file. You
can run the application in this package as described earlier.

The Malhar library of operators
---
In addition to the operators bundled with each demo application,
the Malhar library contains a large number of operators for different
scenarios. In addition to these, you can also write your own operators.
Documentation about the operator library is at <https://docs.datatorrent.com/>.
A tutorial for writing your own operators is at
<https://docs.datatorrent.com/operator_development/>.

Here are some important characteristics of operators:

-   Input data units are arbitrary Java objects that are called tuples or
    events.
-   Operators can, have multiple input and output ports; they receive tuples
    via the input ports and emit tuples via the output ports.
-   An operator may have no ports at all.
-   Input and Output ports are fields defined in an operator; they may
    optionally be annotated using the following tags:
    `@InputPortFieldAnnotation` or `@OutputPortFieldAnnotation`.
-   The type of objects entering an input port is always the same; likewise the
    type of objects leaving an output port is also the same. However, the types
    of objects associated with two different ports can be, and often are, different.
-   All input operators implement the `InputOperator` interface, receive data
    from an external source (not from another operator), and invoke the `emitTuples`
    method to write data to one or more output ports. Since they cannot receive
    data from another operator, they have no input ports.
-   Output operators (there is no OutputOperator interface or base class)
    receive tuples on input ports, process them, and write computed data
    (typically via the `processTuple` method) to external sinks.
-   The vertices of a DAG are operators; the arcs between them are (parts of)
    streams.
-   A single port is connected to a single stream.
-   A stream is connected to one output port of an operator and multiple input
    ports of other operators. Tuples enter the stream through a unique output port
    and are replicated at all the input ports. A stream, therefore, embodies the
    collection of outbound arcs at a single output port of a vertex (operator).
-   The output port that is the common initial end-point of all these arcs is
    called the source of the stream. Similarly, all the input ports at the final
    end-points of these arcs are called sinks. So, a stream has a single source
    but can have multiple sinks.
-   A stream is represented by the `DAG.StreamMeta` interface and is created via
    the `DAG.addStream` method.
-   DAG.StreamMeta has methods `setSource` for the output port, and `addSink`
    for adding input ports.
-   Ports are often created by extending `DefaultOutputPort` and
    `DefaultInputPort`.
