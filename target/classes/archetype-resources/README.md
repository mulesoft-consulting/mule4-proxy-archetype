# ${artifactId}

## DEFINITIONS

| Terme           | description          |
|-----------------|----------------------|
| Branch Name     | is a Git branch name |
| Execution Environment | Each mule app takes a certain amount of initial parameters (e.g credentials or connection keys) and vary from an environment to another. these paremters are store in mule's internal vault and are retrieved depending on the provided environment name|
| Anypoint Environment| The cloudhub environment where applications are running |

## TEMPLATE

### Description

This project is a simple template that integrates some of MuleSoft best practices. It provides a set of standard minimalistic tools that should help you start your project quickly/efficiently.

  - **Plugins**
      - mule-maven-plugin: enriched with a configuration that goes along with the Jenkinsfile (pipeline).
      - maven-release-plugin: maven release management tool see the **Realse** section for more information on how to use it
  - **Structure**
      - Separation between interface and implementation
      - Global configuration file
      - Resources
          - property files: 
            - common property file containing environment variable common to all environments (sandbox to production) like http port, basePath etc ...
            - a property file for each environment DEV/QA/UAT. You can add as many as you want (just don't forget to update the jenkinsfile)
  - **CI/CD**
      - Jenkins: a generic premade pipeline.


## Logging

The application produces logs asynchronously, Following is the anatomy of a log:

```json
{
  "correlationId" : "a5E0E000000Kn6CUAS2021042717273929",
  "message" : "POST WORK UNIT",
  "tracePoint" : "START",
  "priority" : "INFO",
  "elapsed" : 4192,
  "locationInfo" : {
    "lineInFile" : "125",
    "component" : "json-logger:logger",
    "fileName" : "implementation/post-work_unit.xml",
    "rootContainer" : "post:\\work_unit:imp"
  },
  "timestamp" : "2021-04-27T15:27:43.510Z",
  "content" : {
    "key": "value"
  },
  "applicationName" : "s-api-sap-dev-horus",
  "applicationVersion" : "v1.0",
  "environment" : "DEV",
  "threadName" : "[MuleRuntime].uber.5593: [s-api-sap-dev-horus].post:\\work_unit:imp.BLOCKING @68f64e2a"
}
```

| parameters        | description    |
|-------------------|----------------|
| correlationId     | The request correlation ID |
| message           | A basic phrase describing what is the logging about |
| tracePoint        | the check point throughout the flow execution |
| priority          | the log level |
| elapsed           | time elapsed between check points (between START and END for example) |
| locationInfo      | logging location in source code |
| timestamp         | when logging was executed       |
| content           | the logging content or payload  |
| applicationName   | the application's name          |
| applicationVersion | the application's version      |
| environment       | application's execution environment |
| threadName        | the thread name executing the logging task |


**N.B** It is possible to update the logging level whilst the app is running on cloudhub. In fact, you can navigate to your application on Runtime Manager, then go to `settings > Logging` then you can apply the debug level you desire using `org.mule.extension.jsonlogger.JsonLogger` package name.


## RELEASE

In order to prepare a release, execute the following : 

```bash
mvn release:clean release:prepare 
```

You will be prompted to answer a few questions about the release: 

  1) **What is the release version for ...**: the name of the release. should be something like `X.X.X`. Hit enter to accept the default
  2) **What is the SCM release tag or label for ...**: the name of the tag. The default nomenclature is `{project_name}-{version}`. Use the nomenclature `v{version}`, for example `v1.0.5`. Then hit enter.
  3) **What is the new development version for ...**: the development name or the upcoming version you will be working on (the SNAPSHOT version). It should end with `SNAPSHOT`. The pluging automatically increases the patch number. Hit enter. 

You will notice the following temporary files have been created in the root folder : 

  - **release.properties:** contains the release configuration (release tag etc ...)
  - **pom.xml.releaseBackup:** the old content of the `pom.xml` file with the previous release

After you've reviewed the release properties, execute the following to perform the release:

```bash
mvn release:perform 
```
