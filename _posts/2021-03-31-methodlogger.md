---
title: "[Java] A method logger lib with Spring AOP"
date: 2021-03-31 13:53 -0300
categories: java spring aop
permalink: /java-a-method-logger-lib-with-spring-aop
---

MethodLogger is a java lib based in Spring AOP for logging method calls, exposing execution time, serialized returned object and more. This is how you can use it:

## 1. Setup

This lib is available through Jitpack, so if you want to use it just add the Jitpack repo and reference the dependency as follows:
```xml
...
<dependencies>
    ...
    <dependency>
        <groupId>com.github.kelvindules</groupId>
        <artifactId>method-logger</artifactId>
        <version>1.0</version>
    </dependency>
    ...
</dependencies>
...
<repositories>
    ...
    <repository>
        <id>jitpack.io</id>
        <url>https://jitpack.io</url>
    </repository>
    ...
</repositories>
```

## 2. Enabling the lib to be scanned by Spring

To enable MethodLogger, add `@EnableMethodLogger` to your Spring application
```java
@SpringBootApplication
@EnableMethodLogger
public class MyApplication {
	public static void main(String[] args) {
		SpringApplication.run(MyApplication.class, args);
	}
}
```
## 3. Annotate the method

With MethodLogger, just annotate the method you want to be logged with `@LogMethod`

```java
@Component
class AwesomeClass {

    @Autowired
    DummyRepository dummyRepo;

    @LogMethod
    public DummyClass getDummy(final Long id) {
        return dummyRepo.get(id);
    }
}

class DummyClass {
    private String foo;
    private Long bar;
    // getters, setters...
}
```

## 4. When the method is called, this it the default log output:

```json
AwesomeClass -> getDummy(123): [15 ms]
```
With the `show-result` option enabled, you will get it like this:
```json
AwesomeClass -> getDummy(123): {
    "foo": "asdf",
    "bar": 123456
} [15 ms]
```

---
For more details, source at <a href="https://github.com/kelvindules">Github</a>