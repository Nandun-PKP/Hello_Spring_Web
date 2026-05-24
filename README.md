# 🌱 Hello Spring Web - Request Flow Explained

First, let's simply understand the process (flow) of this application:

1. When you enter the link in the browser, it first goes to the **Tomcat Server**.
2. Tomcat first reads the `web.xml` file.
3. It then hands over the incoming request to **Spring**.
4. Spring reads the `spring-dispatcher-servlet.xml` to find out where your codes are located.
5. Finally, the code inside `HelloController.java` executes and sends `"Hello World"` to the browser.

Now let's take them one by one and simply look at what the lines of code inside them mean.

---

## 1. `pom.xml` (The Foundation of the Project)
This is the file read by the Maven software. It downloads the things we need from the internet.

* `<groupId>`, `<artifactId>`, `<version>`: These act as an identity card for your project. (The project name is given here as `hello-spring`).
* `<packaging>war</packaging>`: This is very important. Since we are building a web application, this specifies that all these codes must ultimately be packed into a `.war` (Web Archive) type file.
* `<properties> ... <maven.compiler.source>17...</properties>`: This declares that we are writing code in the Java 17 version.
* `<dependencies>`: This is exactly like a shopping list. It is the list that tells Maven to download the tools we need from the internet and add them to the project, such as the Spring Framework (`spring-webmvc`) and the tools needed to communicate with Tomcat (`javax.servlet-api`).

---

## 2. `web.xml` (The Gatekeeper)
This is the main file that the Tomcat Server reads.

* `<servlet-name>spring-dispatcher</servlet-name>`: We are giving a name to the main controller in Spring as "spring-dispatcher".
* `<servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>`: This is the boss of Spring. It receives every incoming request from the outside.
* `<load-on-startup>1</load-on-startup>`: This is the command to wake up (start) this Spring boss as soon as the Tomcat Server turns on.
* `<url-pattern>/</url-pattern>`: Through this, Tomcat is told, "Send any link (`/`) coming to our website directly to that `spring-dispatcher`, and it will take care of it."

---

## 3. `spring-dispatcher-servlet.xml` (The Brain of Spring)
Now the request has come to Spring. But Spring doesn't know where your codes are located. That is explained by this file.

* `<beans xmlns="...">` *(The long lines at the top)*: These are just a set of rules written in a language that Spring understands. It's like grammar.
* `<context:component-scan base-package="com.example.controller" />`: This is the most important line in this file! This tells Spring, "Go and find the files inside the folder (Package) named `com.example.controller`, read them, and understand what tasks are in them." *(Because our folder was in the wrong place earlier, Spring couldn't read this, which is why we got the 404 Error previously).*

---

## 4. `HelloController.java` (Our Actual Work)
All that background setup was done just to run this file.

* `@Controller`: This is a label (an Annotation) applied so Spring can identify that this is not normal Java code, but a "Controller" connected to a website.
* `@RequestMapping("/hello")`: This sets up a connection so that if someone types `/hello` at the end of the URL in the browser, it should be sent directly to the piece of code (the Method) right below this line.
* `@ResponseBody`: This means "Don't go looking for a separate HTML page; take these words I return and display them directly on the screen of the browser of the person who visited the link."
* `return "Hello World...";`: These are the words that were finally shown on your screen.
