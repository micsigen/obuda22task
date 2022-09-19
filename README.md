# Fibonacci backend service with Spring

This guide walks you through the process of creating a *Fibonacci* number application with Spring.

# What You Will Build

You will build an backend application that will accept HTTP GET requests at: `http://localhost:8080/fibonacci?n=5`.

It will respond a static page that body will contain a *n.* fibonacci number. If the *n* is greater than *46* then return *BAD REQUEST* (500) response code.

The Fibonacci number are represented with the next expression:

```
f(n) = f(n - 1) + f(n - 2)
```

Especially:
```
f(1) = 0
f(2) = 1
f(3) = 1
f(4) = 2
f(5) = 3
f(6) = 5
...
```

# What You Need

- Create a GitHub account if you do not have yet: https://github.com/signup
- Java RE Version 17: https://www.oracle.com/java/technologies/javase/jdk17-archive-downloads.html
- Gradle Version: https://gradle.org/releases/
- Visual Studio Code: https://code.visualstudio.com/download

# Steps

Next steps help to build an contribute the *Fibonacci* application.

## Create a application trunk with Spring Initializr

To manually initialize the project:

- Navigate to https://start.spring.io.
This service pulls in all the dependencies you need for an application and does most of the setup for you.
- Choose Gradle and the language you want to use. This guide assumes that you chose Java.
- Click *Dependencies* and select *Spring Reactive Web*.
- Click *Generate*.
- Download the resulting ZIP file, which is an archive of a web application that is configured with your choices.

NOTE: If your IDE has the Spring Initializr integration, you can complete this process from your IDE.

![Start Spring](src/spring.start.png)

## Create a new project on GitHub

To complete the task needed to create and upload the running trunk application into GitHub. Use the next template to create the project.

![Create a project](src/create.project.png)

## Develop the Fibonacci application

The layers are shown on the next diagram.

![Layers](https://www.plantuml.com/plantuml/png/PL51Jp8n4BttLxmioHSsNwhHen4b63NUzKICAMLO6ifqRRiIGlZlpi82oTf3--RrpRpfT9ooYRbPUnN9PiEL9nGlRXROMEkGAUK2WytI2Lg75M6d573HJYSnR195tF-R7T739qn25xJYwSVRWMeS1bNmSw5gOrUc4gV5oKcRkXOZxwfbdlcczS5X3KiKhy_lk3vB7tcquttHblnkA6w_YETrS9mnM4jHpgPBdJu5pZ5uJn7UR2aUsh1dyYIRDCanfGHf-CTP4jaPTvgUaTP_orm8kUwbSyY4sBxj3eiXbnYr1pHkIlplu6qfuhrIECqEUXusV2Lp4rBsOwo7lMRKNeq5onV-0W00)

### Create a Controller layer

In Spring's approach to building web sites, HTTP requests are handled by a controller. You
can easily identify the controller by the `@RestController` annotation. 

```
@RestController
@RequestMapping("/")
public class FibonacciController {

...

@GetMapping(value = "fibonacci")
    public Integer getFibonacci(@RequestParam Integer n) {
    ...
    }
```

This controller is concise and simple, but there is plenty going on. We break it down step
by step.

The `@GetMapping` annotation ensures that HTTP GET requests to */fibonacci* are mapped to
the `fibonacci()` method.

The `@RequestParam` binds the value of the query string parameter `n` into
the `n` parameter of the `fibonacci()` method. This query string parameter is 
`required`.

### Create Service Layer

In Spring's approach to build business tier is used with `@Component` or `@Service` annotations. In business funtion should be implement the above mentioned Fibonacci number service, that return the n. Fibonacci number.

## Run the Application

After you complete the task you can run the application with the next *Gradle* command.

```
./gradlew.bat bootRun
```

## Test the Application

Following the guideline test the application with two aspects
- With unit tests let us test the service layer. Test the normal cases: `f(1), f(2), ...` and edge cases: `f(-1)`.
- With integration tests let us test controller layer with connected business tier. The the edge case too: `f(47)`.

### Unit tests

Example to test application with *JUnit*:

```
@Test
void shouldReturn0WhenCall1() {
    // given

    // when
    Integer result = underTest.fibonacci(1);
    // then
    Assertions.assertEquals(0, result);
}
```

### Integration tests

Example to test controller layer with *JUnit*

```
@Test
void callFibonacciEndpoint() {
    // given

    // when
    ResponseEntity<String> entity = restTemplate.getForEntity("http://localhost:8080/fibonacci?n=5", String.class);

    // then
    Assertions.assertEquals(HttpStatus.OK, entity.getStatusCode());
    Assertions.assertEquals("3", entity.getBody());
}
```

### Manual test

Now that the web site is running, visit `http://localhost:8080/fibonacci?n=10`, where you should
see "54"
