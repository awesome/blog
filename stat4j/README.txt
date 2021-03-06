Introduction
============

stat4j is Free Software. stat4j is released under the terms of the
Apache, version 2.0 license which may be viewed at:

http://www.apache.org/licenses/LICENSE-2.0

What is stat4j?
===============

stat4j is a a simple,lightweight extension to log4j that allows you to mine your 
logs in real-time for statistical information. It can be used to:
	.Measure and profile application performance
	.Report on business level statistics such as the number of widgets sold
	 or the number of users logged into your site
	.Alert for events that indicate production problems

stat4j may be used by any Java/J2EE application that uses log4j for logging. 
stat4j supports Java 1.4 and above.

Features include:
	.A log4J appender for intercepting log messages
	.A metrics engine for filtering and scraping metrics from log messages
	.Pre-built calculators to dervive statistics using common statistical functions
	.Threshold based alerting
	.An RSS Appender for outputing logs and statistics in RSS format
	
When should you use stat4j?
=========================
.When you want to use a lightweight mechanism for measuring application performance or
 capturing user defined statistics of interest to you or your business
.When you have a mature application and you dont want to use byte code instrumention or 
 invest in exspensive tools
.When you have copious log messages and want to leverage these into useful metrics -
 in real-time

Stat4j is free, production friendly and easy to use. It integrates into your application with 
just one line of configuration.

How does it work? - the 5 second overview
=========================================

Statistics instrumentation:

Statistics may be derived from events or patterns that occur in a log. For example a user count 
may be derived by incrementing a count whenever a messge "User() has logged in."
occurs and decremented whenever a log message "User() has logged out" occurs. Statistics may be be derived from
single (instantaneous) matches or 2 related matches in 2 separate log messages. The unit of measurement 
may be time, memory, occurances or a numeric scraped from the message itself. The stat4j appender
intercepts logs and filters them for matches against user pre-defined statistic patterns. If a match is 
found then the metric is forwarded into stat4j proper which calculates one or more statistic results. 
Calculations can be simple counts,rates or more complex functions such as min,max or average. Log messages that dont 
match any patterns are simply discarded i.e no extra I/O.

Log filtering and scraping is done using regular expressions.

Alerting:

In addition to statistics derivation stat4j allows you to define simple threshold based alerts.
for example WARN when number of users > 100 or error rate > 10 errors per sec. Alerts are evaluated
whenever a statistic is calculated and forwarded to a pre-defined log4j alerts category.
This can then be logged, sent to JMS, or used to generate an RSS feed.

Project Structure
=================
README.txt			Project overview
build.xml			Ant build file
/src				stat4j java source
/test				stat4j junit java source and log configuration
/examples			stat4j examples including and log configuration
/ext				external libraries
/contributors		Comments and src from stat4j contributors
/docs				Docs generated by build
/report				unit test report generated by rruning unit tests

Quick Start
===========

To Build:

stat4j uses ANT to build. Ensure that you have java 1.4+ and ANT installed on you machine.

From the command prompt, cd to the stat4j home directory.

Type "ant list" to get a list of targets to build
Type "ant compile" to compile stat4j classes
Type "ant dist" to build the stat4j jar file
Type "ant test" to runt the stat4j test cases
Type "ant doc" to build the stat4j documentation 
Type "ant demo" to run the stat4j demonstraton app

To Use:

1) Include the stat4j jar file in the classpath of the application you wish to instrument.

e.g java <myApp class> -classpath "libs/log4j.jar;libs/stat4j.jar"

2) Configure log4j to use stat4j

# Add stat4j Appender
log4j.appender.stat4j=net.sourceforge.stat4j.log4j.Stat4jAppender

# Set stat4j Appender as the default appender for your target log categories,
# in this case root. This means all log messages will  be sent to 
# the console and stat4j appenders
log4j.rootCategory=console,stat4j

3) Configure the statistics that you want to measure

stat4j configuration is managed by the stat4j.properties file. This file  
contains the stat4j calculator config and the statistics that you want 
collected.

stat4j will load the stat4j.properties automatically from the classpath when stat4j starts up. 
It is assumed to be at the top of the classpath and so must be present in the
classpath for your application.

stat4j.properties contains several pre-defined statistics,filters 
and alerts: debug_count,error_count,info_count,debug_rate,error_rate, info_rate and error
alert.

To add your own statistics simply follow the examples provided and add your statistics 
configuration to stat4j.properties.

For more information on configuring statistics see the user guide under the docs directory.

For examples that use stat4j see the examples directory.

For more information on log4j setup and configuration see:

	http://logging.apache.org/
	
For more information on ANT see:

	http://ant.apache.org/

Roadmap
=======

1. RSS Appender
2. More Calculators
3. stat4j aspects - to allow statistics collection via AOP
3. Statistics Reporting (push & pull) via RMI/JMX
4. XML configuration
5. User tagging
6. Statistics UI
7. Eclipse Plugin

Contacts
========

stat4j homepage:            http://stat4j.sourceforge.net/
SourceForge project info: 	http://sourceforge.net/projects/stat4j/

