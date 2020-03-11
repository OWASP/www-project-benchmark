---
title: Quick_Start
displaytext: Quick Start
layout:  null
tab: true
order: 3
tags: benchmark
---

## What is in the Benchmark? ##
The Benchmark is a Java Maven project. Its primary component is thousands of test cases (e.g., BenchmarkTest00001.java), each of which is a single Java servlet that contains a single vulnerability (either a true positive or false positive). The vulnerabilities span about a dozen different CWEs currently.

An expectedresults.csv is published with each version of the Benchmark (e.g., expectedresults-1.2.csv) and it specifically lists the expected results for each test case. Here's what the first two rows in this file looks like for version 1.1 of the Benchmark:

```code()
 # test name		category	real vulnerability	CWE	Benchmark version: 1.1	2015-05-22
 BenchmarkTest00001	crypto		TRUE				327
```

This simply means that the first test case is a crypto test case (use of weak cryptographic algorithms), this is a real vulnerability (as opposed to a false positive), and this issue maps to CWE 327. It also indicates this expected results file is for Benchmark version 1.1 (produced May 22, 2015). There is a row in this file for each of the tens of thousands of test cases in the Benchmark. Each time a new version of the Benchmark is published, a new corresponding results file is generated and each test case can be completely different from one version to the next.

The Benchmark also comes with a bunch of different utilities, commands, and prepackaged open source security analysis tools, all of which can be executed through Maven goals, including:

* Open source vulnerability detection tools to be run against the Benchmark
* A scorecard generator, which computes a scorecard for each of the tools you have results files for.

## What Can You Do With the Benchmark? ##
* Compile all the software in the Benchmark project (e.g., mvn compile)
* Run a static vulnerability analysis tool (SAST) against the Benchmark test case code
* Scan a running version of the Benchmark with a dynamic application security testing tool (DAST)
	* Instructions on how to run it are provided below
* Generate scorecards for each of the tools you have results for
	* See the Tool Support/Results page for the list of tools the Benchmark supports generating scorecards for

## Getting Started ##
Before downloading or using the Benchmark make sure you have the following installed and configured properly:

```Shell
GIT: http://git-scm.com/ or https://github.com/
Maven: https://maven.apache.org/  (Version: 3.2.3 or newer works.)
Java: http://www.oracle.com/technetwork/java/javase/downloads/index.html (Java 7 or 8) (64-bit)
```

## Getting, Building, and Running the Benchmark ##
To download and build everything:

```Shell
$ git clone https://github.com/OWASP/benchmark 
$ cd benchmark
$ mvn compile   (This compiles it)
$ runBenchmark.sh/.bat - This compiles and runs it.
```

Then navigate to: https://localhost:8443/benchmark/ to go to its home page. It uses a self signed SSL certificate, so you'll get a security warning when you hit the home page.

Note: We have set the Benchmark app to use up to 6 Gig of RAM, which it may need when it is fully scanned by a DAST scanner. The DAST tool probably also requires 3+ Gig of RAM. As such, we recommend having a 16 Gig machine if you are going to try to run a full DAST scan. And at least 4 or ideally 8 Gig if you are going to play around with the running Benchmark app.

## Using a VM instead ##
We have several preconstructed VMs or instructions on how to build one that you can use instead:
* Docker: A Dockerfile is checked into the project here. This Docker file should automatically produce a Docker VM with the latest Benchmark project files. After you have Docker installed, cd to /VMs then run:
```Shell
./buildDockerImage.sh --> This builds the Docker Benchmark VM (This will take a WHILE)
docker images  --> You should see the new benchmark:latest image in the list provided
# The Benchmark Docker Image only has to be created once. 
```
To run the Benchmark in your Docker VM, just run:
```Shell
  ./runDockerImage.sh  --> This pulls in any updates to Benchmark since the Image was built, builds everything, and starts a remotely accessible Benchmark web app.
```
If successful, you should see this at the end:
```Shell
  [INFO]_[talledLocalContainer] Tomcat 8.x started on port [8443]
  [INFO] Press Ctrl-C to stop the container...
```
Then simply navigate to: https://localhost:8443/benchmark from the machine you are running Docker

Or if you want to access from a different machine:
```Shell
 docker-machine ls (in a different terminal) --> To get IP Docker VM is exporting (e.g., tcp://192.168.99.100:2376)
 Navigate to: https://192.168.99.100:8443/benchmark in your browser (using the above IP as an example)
```
* Amazon Web Services (AWS) - Here's how you set up the Benchmark on an AWS VM:

```Shell
sudo yum install git
sudo yum install maven
sudo yum install mvn
sudo wget http://repos.fedorapeople.org/repos/dchen/apache-maven/epel-apache-maven.repo -O /etc/yum.repos.d/epel-apache-maven.repo
sudo sed -i s/\$releasever/6/g /etc/yum.repos.d/epel-apache-maven.repo
sudo yum install -y apache-maven
git clone https://github.com/OWASP/benchmark
cd benchmark
chmod 755 *.sh
./runBenchmark.sh -- to run it locally on the VM.
./runRemoteAccessibleBenchmark.sh -- to run it so it can be accessed outside the VM (on port 8443).
```

## Running Free Static Analysis Tools Against the Benchmark ##
There are scripts for running each of the free SAST vulnerability detection tools included with the Benchmark against the Benchmark test cases. On Linux, you might have to make them executable (e.g., chmod 755 *.sh) before you can run them.

Generating Test Results for PMD:
    ./scripts/runPMD.sh (Linux) or .\scripts\runPMD.bat (Windows)

Generating Test Results for FindBugs:
    ./scripts/runFindBugs.sh (Linux) or .\scripts\runFindBugs.bat (Windows)

Generating Test Results for FindBugs with the FindSecBugs plugin:
    ./scripts/runFindSecBugs.sh (Linux) or .\scripts\runFindSecBugs.bat (Windows)

In each case, the script will generate a results file and put it in the /results directory. For example:
    Benchmark_1.2-findbugs-v3.0.1-1026.xml

This results file name is carefully constructed to mean the following: It's a results file against the OWASP Benchmark version 1.2, FindBugs was the analysis tool, it was version 3.0.1 of FindBugs, and it took 1026 seconds to run the analysis.

NOTE: If you create a results file yourself, by running a commercial tool for example, you can add the version # and the compute time to the filename just like this and the Benchmark Scorecard generator will pick this information up and include it in the generated scorecard. If you don't, depending on what metadata is included in the tool results, the Scorecard generator might do this automatically anyway.

## Generating Scorecards ##
The scorecard generation application BenchmarkScore is included with the Benchmark. It parses the output files generated by any of the supported security tools run against the Benchmark and compares them against the expected results, and produces a set of web pages that detail the accuracy and speed of the tools involved. For the list of currently supported tools, check out the: Tools Support/Results tab. If you are using a tool that is not yet supported, simply send us a results file from that tool and we'll write a parser for that tool and add it to the supported tools list.

The following command will compute a Benchmark scorecard for all the results files in the /results directory. The generated scorecard is put into the /scorecard directory.
```Shell
createScorecard.sh (Linux) or createScorecard.bat (Windows)
```
An example of a real scorecard for some open source tools is provided at the top of the Tool Support/Results tab so you can see what one looks like.

We recommend including the Benchmark version number in any results file name, in order to help prevent mismatches between the expected results and the actual results files. A tool will not score well against the wrong expected results.

**Customizing Your Scorecard Generation**

The createScorecard scripts are very simple. They only have one line. Here's what the 1.2 version looks like:
```Shell
mvn validate -Pbenchmarkscore -Dexec.args="expectedresults-1.2.csv results"
```
This Maven command simply says to run the BenchmarkScore application, passing in two parameters. The 1st is the Benchmark expected results file to compare the tool results against. And the 2nd is the name of the directory that contains all the results from tools run against that version of the Benchmark. If you have tool results older than the current version of the Benchmark, like 1.1 results for example, then you would do something like this instead:
```Shell
mvn validate -Pbenchmarkscore -Dexec.args="expectedresults-1.1.csv 1.1_results"
```
To keep things organized, we actually put the expected results file inside the same results folder for that version of the Benchmark, so our command looks like this:
```Shell
mvn validate -Pbenchmarkscore -Dexec.args="1.1_results/expectedresults-1.1.csv 1.1_results"
```
In all cases, the generated scorecard is put in the /scorecard folder.

**WARNING: If you generate results for a commercial tool, be careful who you distribute it to. Each tool has its own license defining when any results it produces can be released/made public. It is likely to be against the terms of a commercial tool's license to publicly release that tool's score against the OWASP Benchmark. The OWASP Benchmark project takes no responsibility if someone else releases such results.** It is for just this reason that the Benchmark project isn't releasing such results itself.
