# Maven Archetype for Mule4 Proxy Application

## How to use 

```
mvn archetype:generate \
  -DarchetypeGroupId=org.mulesoft\
  -DarchetypeArtifactId=mule-proxy-archetype \
  -DarchetypeVersion=1.0.0-SNAPSHOT \
  -DgroupId=8d3ba7c8-5ec7-4dde-bc43-20ddb7f700aa \
  -DartifactId=x-api-vasco-product \
  -DcontrolPlane=eu \
  -Dregion=eu-central-1 \
  -DdeployTarget=rtf \
  -DdeployAuthType=server \
  -Dscmtype=git \
  -DscmRepository=git@github.com:user/repo \
  -DpluginJsonLogger=8a67cc18-61b1-4ef6-9d51-eb15886ae7e3 \
  -DpluginJsonLoggerVersion=2.0.1
```