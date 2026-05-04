# codeartifact-maven-extension

Fork of https://github.com/dangernoodle-io/codeartifact-maven-extension

![maven](https://img.shields.io/maven-central/v/dev.bcmedeiros/codeartifact-maven-extension)

Maven `build` extension that provides a [resolver](https://maven.apache.org/resolver/index.html) and 
[wagon](https://maven.apache.org/wagon/index.html) implementation capable of authenticating against 
[AWS CodeArtifact](https://aws.amazon.com/codeartifact/) before uploading/downloading artifacts.

Java 8 or greater is required. The appropriate implementation will automatically be selected based upon your maven
version. See [here](https://maven.apache.org/guides/mini/guide-resolver-transport.html) for additional details.

## Usage

The easiest way to configure the plugin is to add an entry to the `.mvn/extensions.xml` file (see [here](https://maven.apache.org/configure.html)
for more details) like so:

```xml
<extensions xmlns="http://maven.apache.org/EXTENSIONS/1.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/EXTENSIONS/1.0.0 http://maven.apache.org/xsd/core-extensions-1.0.0.xsd">
  <extension>
     <groupId>dev.bcmedeiros</groupId>
     <artifactId>codeartifact-maven-extension</artifactId>
     <version>${codeartifact-maven-extension.version}</version>
  </extension>
</extensions>
```

This is the recommended approach if you use a parent pom that is also stored within `codeartifact`. If you have a
standalone project and don't wish to use the `.mvn` directory, you can add the following to the build section of 
your project's pom:

```xml

<build>
  <extensions>
    <extension>
      <groupId>dev.bcmedeiros</groupId>
      <artifactId>codeartifact-maven-extension</artifactId>
      <version>${codeartifact-maven-extension.version}</version>
    </extension>
  </extensions>
  ...
</build>
```

### Credentials

The extension automatically uses the [DefaultCredentialsProvider](https://sdk.amazonaws.com/java/api/latest/software/amazon/awssdk/auth/credentials/DefaultCredentialsProvider.html) to find AWS credentials. Be sure you have 
configured your environment accordingly.

Separately, static credentials can be provided in an a `server` entry in `maven-settings.xml`

```xml

<servers>
  <server>
    <id>codeartifact</id>
    <username>AWS_ACCESS_KEY_ID</username>
    <password>AWS_SECRET_ACCESS_KEY</password>
  </server>
</servers>
```

Make sure you are using appropriate security precautions if you are using static credentials.
