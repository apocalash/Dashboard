
# HealthCheck

The Health Check POC is a two part application consisting of a Health Check Module and a Dashboard.
1. The Health Check Module is a Spring Boot-based module for health checking and monitoring applications. It can be integrated with existing applications as a Spring dependency. 
The module opens up custom actuator endpoints that can be used to check up on various health statistics of the application. 

2. The Dashboard, an Angular webpage is used to display these custom actuator endpoints in a visual manner. The dashboard invokes the actuator endpoints dynamically based on the application URL and refreshes the data in fixed intervals.


   
## Getting Started
To implement the Health Check Module with your existing applications, the following steps are be followed -



### Pre-Requities
* Java Version - 17 
* Maven as build tool
* Spring Boot Application
### Configuration
The following configurations must be added, if not already present in the application.properties file: 

```
#mention the name of your application here
spring.application.name =       

#mention the port number your application uses
server.port =       

#database connectivity details
spring.datasource.url = 
spring.datasource.username = 
spring.datasource.password = 
spring.datasource.driver-class-name = 
spring.jpa.hibernate.ddl-auto = 

#to allow cross origin referencing
management.endpoints.web.cors.allowed-origins = *
```
### Installation

To use the the Health Check Module in your Spring Boot application, you can add the following Maven dependency to the pom.xml file of your project:

```xml
<dependency>
    <groupId>com.nissan</groupId>
    <artifactId>healthcheck</artifactId>
    <version>0.0.3-SNAPSHOT</version>
</dependency>
``` 

### Integration
1. Add Dependency:
Add the module dependency to your project as shown in the installation instructions.

2. Use in Your Application:
Once the dependency has been added to the pom.xml file, you must reload all maven project. Once dependency has been loaded to your application successfully, you can add the annotation to the main application class or any other Spring components:
``` java
@EnableHealthCheckModule
```
This annotation will invoke the dependency and the expose all the actuator endpoints which can be used to visualize the details of the application.


## Dependency Usage

The below is an sample usage of the Health Check Module that has been added as a dependency to the TestApplication and being invoked using the custom annotation.

```java
import com.nissan.healthcheck.annotation.EnableHealthCheckModule;
import com.nissan.healthcheck.controller.Dashboard;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
@EnableHealthCheckModule    //annotation to invoke the dependency
public class TestApplication {

	public static void main(String[] args) {
		SpringApplication.run(TestApplication.class, args);

	}
}
```

## Endpoints Implementation
The following Endpoints have been initialized as part of the Health Check Module to help obtain various information about the application the dependency has been added to -

1. Application Name - used to provide the name of the application as configured in the properties file of the application.

2. Status - visual showcase of whether the application is running successfuly or not.

3. Backend Info - provides the information related to the backend technology being used in this application and its version.

4. System Info - details about the amount of CPU usage by the application and the total available processor counts to the JVM.

5. Application Uptime - total runtime of the application since it's execution started.

6. Database Info - shows the database that's connected to the application and it's version.

7. Memory Usage - the amount of total available memory, max memory and used memory of the application.

8. Java Version - the version of Java the application uses.

9. Process Id - the internal process id of the application.

10. Port Info - the server port number the application uses.

11. Memory dump - a downloadable file that provides the entire memory dump of the application that can be used for futher analyses. 

## Dashboard
The dashboard for visualizing the applications is made using Angular to help create a dynamic webpage that can be used to visualize the various health data of the application.

The user is required to input the name of the application along with the URL in which the application is hosted (ex: localhost:8080) which would then fetch the data from the different actuator endpoints pertaining to that application and display them out in the form of a dashboard.

Multiple applications can be added and viewed in a seqential manner.

## Screenshot
The dashboard representing the health details of the application which has been invoked using the custom actuator endpoints would appear in this manner -

![Dashboard Screenshot](dashboard_ss.png)

## Authors

- Poornachandran, Krittika
- Ranganathan, Simmavakeesvar
- Philip, Ashish


