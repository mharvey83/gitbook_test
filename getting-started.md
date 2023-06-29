# Getting Started

Simprints ID is our standalone app that lets you capture biometrics for purposes of enrolment, identification and verification. You communicate with the Simprints ID using [Android intents](https://developer.android.com/guide/components/intents-filters). To see an overview of what happens [check here](broken-reference).

Using our open-source helper library, [LibSimprints](https://github.com/Simprints/LibSimprints), you can easily integrate Simprints ID with your custom android application. To start with the integration, you will first add the library as a dependency to your android project.

Installation

NOTE:  Ensure you are installing the latest version of LibSimprints, you can check our [releases page](https://github.com/Simprints/LibSimprints/releases) for the latest version.&#x20;

For Gradle:

implementation "com.simprints:libsimprints:2023.2.1"

For Maven:

\<dependency>

\<groupId>com.simprints\</groupId>

\<artifactId>libsimprints\</artifactId>

\<version>2023.2.1\</version>

\<type>pom\</type>

\</dependency>&#x20;

Basic Features

Simprints ID supports 3 basic features: Enrolment, Identification, and Verification.

\


1. [Enrolment](broken-reference) - this is a process that involves registering a new beneficiary, using their biometric data.
2. [Identification](broken-reference) - this is a process that involves identifying a beneficiary from a list of matching candidates.
3. [Verification](broken-reference) -  this involves verifying that a beneficiary is who they say they are.

Note:  any call to Simprints ID should be triggered after capturing the user's personal information, i.e. on form submission, so the last action is the biometric capture.

### &#x20;<a href="#h.p9jskyd3pz3m_l" id="h.p9jskyd3pz3m_l"></a>

Since Simprints ID is a standalone application, when integrating with Simprints ID your Android application communicates with Simprints ID through [Android Intents](https://developer.android.com/guide/components/intents-filters).

This process requires some basic parameters to be sent in the corresponding intent. Here is a list of request parameters you would encounter when integrating with Simprints ID, what they stand for, and what they are used for:

\


* Project ID  -  this is a unique id that is generated for your project during integration with Simprints ID and is used for integration purposes as well as authentication. As you can have multiple projects, to target different solutions, each project has its own unique id which is the project ID.

\


* Module ID   -  this can be used to stratify a dataset. During an identification, large datasets (e.g. project-wide) can take longer to search for a match and reduce accuracy. Having modules will help run the identification in smaller datasets. Common modules include sub-district, school or health facility. We recommend each module does not exceed 15,000 registrations

This module id is a unique id that represents any specific module (geographical location), where the frontline worker is capturing biometrics for enrolment, identification, or verification.

\


* User ID  -  This is a unique id that represents the logged-in user who attends to the beneficiaries during the biometric capture. This is specific to your app.

\


* Session ID  -  This is a unique id that is generated for every Simprints ID initiated flow, i.e. enrolment, identification, or verification. It is used to track each flow from start to finish.
