# README #

This README gives an overview about the sor-client-sdk library.

----------------------------------------------------
### Index
* [What is this repository for ?](#What-is-this-repository-for?)
  * [Overview](#overview)
  * [Versioning](#versioning)
* [Code at Client's side to trigger the flow ?](#code-at-Client-side-to-trigger-the-flow?)
* [All About Request and Response](#all-about-Request-and-Response)
* [Loggers](#loggers)
* [How do I get set up?](#how-do-I-get-set-up?)
* [Exception Handling](#exception-handling)
  * [Credit and Debit API Response Codes](#credit-and-debit-api-response-codes)
  * [Status Check API Response Codes](#status-check-api-response-codes)
* [Why to add this library ?](#why-to-add-this-library?)
* [Contribution guidelines](#contribution-guidelines)
* [Whom do I talk to ?](#whom-do-I-talk-to?)

----------------------------------------------------

### What is this repository for?

#### Overview

* sor-client-sdk is a library written in Java using Maven.Spring has been introduced to cover certain aspects which makes the
  communication with SOR APIs easier.

* sor-client-sdk does the job of communication with SOR Credit/Debit and Status Check API on behalf of the client.
  All the communication related stuff such as Rest Template, request/response parsing are handled by the library itself.

* The library aims to make your work easy and saves ample of duplicated code at the client side.  

#### Versioning

* If any change is made in the library, it will be published as latest only. You don't to worry about the versioning.

----------------------------------------------------

### Code at Client side to trigger the flow?

* Inside the test/java/in.nbt.sor.sdk/client directory there are two classes that provide the actual code that client 
  has to write at its end. In order to call the SOR's status check/ Credit Debit Api. Please refer to SorCreditDebitLibClient 
  and SorStatusCheckLibClient for Java code to invoke the library flow and request/response related stuff.

  &nbsp; &nbsp; &nbsp; &nbsp; [Click to redirect to test package](https://bitbucket.org/paynearyby/sor-client-sdk/src/develop/src/test/java/in/nbt/sorsdk/client/).

* Also, this can be found in detail in the following google document.

----------------------------------------------------

### All about Request and Response

* Please refer to the document for Request and Response structure :- _https://drive.google.com/file/d/1l8FlVEjBGXrBktSp4REvDU9ZxRvV7N90/view?usp=drive_link_

* For valid acceptable values to be passed in fields, please have a look at this document :- _https://drive.google.com/file/d/1ByIaxCDahxs_4kOfiYdKsPHs4NiqHbrb/view?usp=drive_link_

----------------------------------------------------

### Loggers

* Logging is an essential part of the system in order to track the transactions in real-time. All the loggers
  of the library are populated in the client's log file under heading _**logger_name : sor-client-sdk**_. This gives a clear indication to the client
  about its own logs and the ones coming from the library.

----------------------------------------------------

### How do I get set up?

* Just add the following dependency in your pom.xml / build.gradle as per your Java project. It will be downloaded from JFrog and
  will be injected as an external library in your project.

----------------------------------------------------

_Java maven artifact (*maintenance mode*):_
```xml
<dependency>
   <groupId>in.nbt.sorsdk</groupId>
   <artifactId>sor-client-sdk</artifactId>
   <version>latest</version>
</dependency>
```
Or [download from here](https://paynearby.jfrog.io/ui/repos/tree/General/sor-client-sdk-libs-snapshot-local).

----------------------------------------------------

### Exception Handling

* The library internally validates the request sent by the client. If it's not valid then ValidationException
  (an internal exception class of the library) is thrown.
  Rest of all kinds of exception are directly thrown to the client's caller method.
  Along with that, the library returns the response codes as it was from the SOR's end. It includes the following :- <br/>

----------------------------------------------------

#### Credit and Debit API Response Codes
            
            | Resp Code | Resp Message             |
            |-----------|--------------------------|
            | 0         | Success                  |
            | 100       | Invalid Agent            |
            | 100       | Agent Blocked status     |
            | 100       | Balance Not Available    |
            | 100       | System under Maintenance |
            | 201       | Entry Already Available  |
            | 501 - 599 | Input JSON Validation    |
            | 500       | Internal Exception       |

#### Status Check API Response Codes
            
            | Resp Code | Resp Message             |
            |-----------|--------------------------|
            | 0         | Success                  |
            | 100       | Invalid Agent            |
            | 100       | Agent Blocked status     |
            | 100       | Balance Not Available    |
            | 301       | Transaction not exist    |
            | 501 - 599 | Input JSON Validation    |

----------------------------------------------------

### Why to add this library?

* The library communicates with the SOR system on client's behalf. Clients don't have to worry about the configuration
  and pool related stuff.The library uses Rest Template internally to call SOR's APIs.Configuration pool props of Rest Template
  are kept optional. If, not provided by the client then the following default values are used.

  &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; MAX CONNECTIONS = 2000 <br/>
  &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; MAX CONNECTIONS PER ROUTE = 2000 <br/>
  &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; CONNECTION TIMEOUT = 3000 <br/>
  &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; READ WRITE TIMEOUT = 60000 <br/>

* Parsing of SOR Request and Response is done internally by the library. Client has to pass the SorGenericRequest / StatusCheckGenericRequest as the input
  and the library returns an SorGenericResponse with simplified fields such as income,tds,product details etc. to the client.

* Handling of edge cases and exception scenarios is completely handled by the library at every layer.The client
  only needs to entertain the Validation Exception/ RestClient Exceptions / Exceptions that are coming directly from the SOR's end.

* All the DTOs of request and response are there in the library itself. So, the clients don't have to worry about the creation of
  multiple classes in order to prepare the request. It saves huge amount of code at the client's end. Also, if the same application
  deals with SOR apis through various services then no need to inject any DTO in all of them. Simply, invoke the library.

----------------------------------------------------

### Contribution Guidelines

* SonarQube Link :- _https://sonarqube.paynearby.in/dashboard?id=sor-client-sdk-maven-uat_
* JFrog Link :- _https://paynearby.jfrog.io/ui/repos/tree/General/sor-client-sdk-libs-snapshot-local_

----------------------------------------------------

### Whom do I talk to?

* For any concerns/suggestions feel free to reach out to us at :- _**aeps-dev@paynearby.in**_

  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **HAPPY LEARNING :)**