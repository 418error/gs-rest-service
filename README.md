# gs-rest-service

#### Built using...
* A Mac
* Atom
* Java JDK 1.8
* Gradle 2.10

#### The steps...

1. Create a project folder

  ```
  mkdir gs-rest-service
  cd gs-rest-service
  ```
2. Create a Gradle build script
  ```
  touch build.gradle
  atom build.gradle
  ```
  Copy the contents from this [Initial Gradle build script](  https://github.com/spring-guides/gs-rest-service/blob/master/initial/build.gradle) to the build.gradle file

3. Create the project directory structure
  ```
  mkdir -p src/main/java/hello
  ```

4. Create a resource representation class
  ```
  touch src/main/java/hello/Greeting.java
  atom src/main/java/hello/Greeting.java
  ```
  Add the following

  ```java
  package hello;

  public class Greeting {

      private final long id;
      private final String content;

      public Greeting(long id, String content) {
          this.id = id;
          this.content = content;
      }

      public long getId() {
          return id;
      }

      public String getContent() {
          return content;
      }
  }
  ```
5. Create a resource controller
  ```
  touch src/main/java/hello/GreetingController.java
  atom src/main/java/hello/GreetingController.java
  ```

  Add the following
  ```java
  package hello;

  import java.util.concurrent.atomic.AtomicLong;
  import org.springframework.web.bind.annotation.RequestMapping;
  import org.springframework.web.bind.annotation.RequestParam;
  import org.springframework.web.bind.annotation.RestController;

  @RestController
  public class GreetingController {

      private static final String template = "Hello, %s!";
      private final AtomicLong counter = new AtomicLong();

      @RequestMapping("/greeting")
      public Greeting greeting(@RequestParam(value="name", defaultValue="World") String name) {
          return new Greeting(counter.incrementAndGet(),
                              String.format(template, name));
      }
  }
  ```
6. Make it executable
  ```
  touch src/main/java/hello/Application.java
  atom src/main/java/hello/Application.java
  ```
  Add the following

  ```java
  package hello;

  import org.springframework.boot.SpringApplication;
  import org.springframework.boot.autoconfigure.SpringBootApplication;

  @SpringBootApplication
  public class Application {

      public static void main(String[] args) {
          SpringApplication.run(Application.class, args);
      }
  }
  ```
7. Run it
  * The one liner
  ```
  gradle bootRun
  ```
  * Build and run
  ```
  gradle Build
  java -jar build/libs/gs-rest-service-0.1.0.jar
  ```

8. Test the thing

  <http://localhost:8080/greeting>
  ```
  {"id":1,"content":"Hello, World!"}
  ```
  <http://localhost:8080/greeting?name=bob>
  ```
  {"id":2,"content":"Hello, bob!"}
  ```
