# Fibonacci backend service with Spring

This guide walks you through the process of creating a "`Fibonacci`" application with Spring.

# What You Will Build

You will build an backend application that will accept HTTP GET requests at: `http://localhost:8080/fibonacci?n=5`.

It will respond a static page that body will contain a n. fibonacci number.

# What You Need

Java version: 17
Visual Code: 

# Steps
## Starting with Spring Initializr

You can use this 

To manually initialize the project:

. Navigate to https://start.spring.io.
This service pulls in all the dependencies you need for an application and does most of the setup for you.
. Choose Gradle and the language you want to use. This guide assumes that you chose Java.
. Click *Dependencies* and select *Spring Web*.
. Click *Generate*.
. Download the resulting ZIP file, which is an archive of a web application that is configured with your choices.

NOTE: If your IDE has the Spring Initializr integration, you can complete this process from your IDE.

NOTE: You can also fork the project from Github and open it in your IDE or other editor.

## Create a Controller

In Spring's approach to building web sites, HTTP requests are handled by a controller. You
can easily identify the controller by the {Controller}[`@Controller`] annotation. In the
following example, `GreetingController` handles GET requests for `/greeting` by returning
the name of a {View}[`View`] (in this case, `greeting`). A `View` is responsible for
rendering the HTML content. The following listing (from
`src/main/java/com/example/servingwebcontent/GreetingController.java`) shows the
controller:

This controller is concise and simple, but there is plenty going on. We break it down step
by step.

The `@GetMapping` annotation ensures that HTTP GET requests to `/fibonacci` are mapped to
the `fibonacci()` method.

{RequestParam}[`@RequestParam`] binds the value of the query string parameter `n` into
the `name` parameter of the `greeting()` method. This query string parameter is not
`required`. If it is absent in the request, the `defaultValue` of `World` is used. The
value of the `name` parameter is added to a {Model}[`Model`] object, ultimately making it
accessible to the view template.

## Run the Application


## Test the Application

Now that the web site is running, visit `http://localhost:8080/fibonacci?n=10`, where you should
see "54"
