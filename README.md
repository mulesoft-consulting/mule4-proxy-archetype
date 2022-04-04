# Maven Archetype for Mule4 Proxy Application

## How to use 

1. Clone the release of your choice
2. Install the project using the following command
  ```
    mvn clean install
  ```
3. Use the archetype with the following command (replace values according to your use case)

  ```
  mvn archetype:generate \
    -DarchetypeGroupId=org.mulesoft\
    -DarchetypeArtifactId=mule-proxy-archetype \
    -DarchetypeVersion=1.0.0 \
    -DgroupId=<YOUR_ANYPOINT_BG> \
    -DartifactId=<YOUR_PROJECT_NAME> \
    -DcontrolPlane=eu \
    -Dregion=eu-central-1 \
    -DdeployTarget=rtf \
    -DdeployAuthType=server
  ```

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