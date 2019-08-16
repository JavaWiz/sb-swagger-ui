# Spring Boot RESTful API Documentation With Swagger 2

## Overview
When creating a REST API, good documentation is instrumental.

Moreover, every change in the API should be simultaneously described in the reference documentation. Accomplishing this manually is a tedious exercise, so automation of the process was inevitable.

In this example, we will look at Swagger 2 for a Spring REST web service. For this example, we will use the Springfox implementation of the Swagger 2 specification.

## Adding the Maven Dependency
As mentioned above, we will use the Springfox implementation of the Swagger specification. The latest version can be found on Maven Central.

To add it to our Maven project, we need a dependency in the pom.xml file.

```
<dependency>
	<groupId>io.springfox</groupId>
	<artifactId>springfox-swagger2</artifactId>
	<version>2.9.2</version>
</dependency>
```

## Integrating Swagger 2 into the Project

### Java Configuration

```
@Configuration
@EnableSwagger2
public class SwaggerConfig {                                    
    @Bean
    public Docket api() { 
        return new Docket(DocumentationType.SWAGGER_2)  
          .select()                                  
          .apis(RequestHandlerSelectors.any())              
          .paths(PathSelectors.any())                          
          .build();                                           
    }
}
```

<b>Swagger 2 is enabled through the @EnableSwagger2 annotation.</b>

After the Docket bean is defined, its select() method returns an instance of ApiSelectorBuilder, which provides a way to control the endpoints exposed by Swagger.

Predicates for selection of RequestHandlers can be configured with the help of RequestHandlerSelectors and PathSelectors. Using any() for both will make documentation for your entire API available through Swagger.

<b>This configuration is enough to integrate Swagger 2 into an existing Spring Boot project.</b> For other Spring projects, some additional tuning is required.

## Verification
To verify that Springfox is working, you can visit the following URL in your browser:

<a href="http://localhost:8080/v2/api-docs">http://localhost:8080/v2/api-docs</a>

The result is a JSON response with a large number of key-value pairs, which is not very human-readable. Fortunately, Swagger provides Swagger UI for this purpose.

## Swagger UI
Swagger UI is a built-in solution which makes user interaction with the Swagger-generated API documentation much easier.

## Enabling Springfox’s Swagger UI
To use Swagger UI, one additional Maven dependency is required:

```
<dependency>
    <groupId>io.springfox</groupId>
    <artifactId>springfox-swagger-ui</artifactId>
    <version>2.9.2</version>
</dependency>
```

Now you can test it in your browser by visiting http://localhost:8080/swagger-ui.html

In our case, by the way, the exact URL will be: http://localhost:8080/swagger-ui.html

## Exploring Swagger Documentation

Within Swagger’s response is a list of all controllers defined in your application. Clicking on any of them will list the valid HTTP methods (DELETE, GET, HEAD, OPTIONS, PATCH, POST, PUT).

Expanding each method provides additional useful data, such as response status, content-type, and a list of parameters. It is also possible to try each method using the UI.