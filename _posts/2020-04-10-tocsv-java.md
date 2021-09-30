---
title: "[Java] CSV Builder Class"
date: 2020-04-10 23:16:00 -0300
permalink: /java-csv-builder-class
---

tocsv-java is a csv builder class.

#### how to use

```java
Foo foo = new Foo();
foo.setA(1);
foo.setB(1.1);
foo.setC("bar");
String csv = EasyCSV.builder()
    .setSource(foo)
    .build();
```

#### output

```
A,B,C
1,1.1,bar
```

#### Currently supported types

* all primitive/wrapper types.
* java.lang.String
* java.util.Date

#### Supporting custom types

tocsv-java uses a registry class named FormatterRegistry which loads and manages the formatters. 

In order for it to load your custom formatter, 
you need to implement **FieldFormatter** and add a line with the package name to the service configuration file at *main/resources/dev.dules.FieldFormatter*. 

Important: Custom formatters have priority over the already supported primitive/wrapper types, overriding it's behavior.

---
for more details, source at <a href="https://github.com/kelvindules/tocsv-java.git" target="_blank">Github</a>
