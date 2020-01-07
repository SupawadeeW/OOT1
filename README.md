# 1. Create project using maven command
```
mvn archetype:generate -DgroupId=th.ac.kmitl.it.oot.www -DartifactId=MyWebApp -DarchetypeArtifactId=maven-archetype-webapp -DinteractiveMode=false
```
### Note!!
```DgroupId``` is your package name. Package names are written in all lower case to avoid conflict with the names of classes or interfaces.

Companies use their reversed Internet domain name to begin their package names—for example, com.example.mypackage for a package named mypackage created by a programmer at example.com.

Name collisions that occur within a single company need to be handled by convention within that company, perhaps by including the region or the project name after the company name (for example, com.example.region.mypackage).

Packages in the Java language itself begin with java. or javax.

In some cases, the internet domain name may not be a valid package name. This can occur if the domain name contains a hyphen or other special character, if the package name begins with a digit or other character that is illegal to use as the beginning of a Java name, or if the package name contains a reserved Java keyword, such as "int". In this event, the suggested convention is to add an underscore. For example:

| Domain Name         | Package Name Prefix  |
|---------------------|----------------------|
| oot.it.kmitl.ac.th  | th.ac.kmitl.it.oot   |
| example.int         | int_.example         |
| 123name.example.com | com.example._123name |

```DartifactId``` is your application name. It will releate to your end production application.

```DarchetypeArtifactId``` is type of application. We use ```maven-archetype-webapp``` to create basic application, and code structure. You can study more about this at [https://maven.apache.org/guides/introduction/introduction-to-archetypes.html]()

# 2. Add plugin for run application
You can compile/build your application using command as follow.

```
mvn package
```

To run application, you can use java command, For example.,

```
java -cp target/MyWebApp-1.0-SNAPSHOT.jar th.ac.kmitl.it.oot.webapp.App
```
Where ```MyWebApp``` is your application name, and ```-1.0-SNAPSHOT``` is your application version (reference and config in pom.xml). And ```th.ac.kmitl.it.oot.webapp.App``` is package that contain main function.

To make it easier you can use plugin, by add plugin to your ```pom.xml```.

``` xml
<build>
    <finalName>MyWebApp</finalName>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.8.1</version>
            <configuration>
                <source>1.8</source>
                <target>1.8</target>
            </configuration>
        </plugin>
        <plugin>
            <groupId>org.eclipse.jetty</groupId>
            <artifactId>jetty-maven-plugin</artifactId>
            <version>9.4.7.v20170910</version>
            <configuration>
                <httpConnector>
                    <port>8888</port>
                </httpConnector>
                <webApp>
                    <contextPath>/${project.build.finalName}</contextPath>
                </webApp>
                <stopKey>CTRL+C</stopKey>
                <stopPort>8999</stopKey>
                <scanIntervalSeconds>10</scanIntervalSeconds>
                <scanTargets>
                    <scanTarget>src/main/webapp/WEB-INF/web.xml</scanTarget>
                </scanTargets>
            </configuration>
        </plugin>
    </plugins>
</build>
```

After install plugin, Now you can run your application using 

```
mvn exec:java
```
!Note, If you update your application. You still need to run ```mvn package``` before run application.