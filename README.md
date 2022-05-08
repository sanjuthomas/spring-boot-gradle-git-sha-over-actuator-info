## Git commit sha over Spring boot actuator info [gradle project example]

Tired of asking what version is running in QA/UAT/PROD? Make your life simple through the actuator/info and git-commit-id plugin.

There are only four simple changes you have to make to expose git commit sha over actuator/info endpoint.

1. Add ```org.springframework.boot:spring-boot-starter-actuator``` to build.gradle
   
2. Enable Spring actuator/info endpoint through adding following configuration to application.yml

```
   management.endpoints.web.exposure.include: info
```

3. Add [gradle-git-properties](https://plugins.gradle.org/plugin/com.gorylenko.gradle-git-properties) plugin to application's build.gradle

```
    'com.gorylenko.gradle-git-properties' version '2.4.1'
```

4. Add following Spring boot plugin DSL to build.gradle

```
    springBoot {
        buildInfo()
    }
```

Build the application using gradle and start the application. We are done! Check out your application's actuator/info endpoint. You should see a JSON like the following -

```
   {
       "git":{
          "branch":"main",
          "commit":{
             "id":"0f411eb",
             "time":"2022-05-08T14:58:02Z"
          }
       },
       "build":{
          "artifact":"demo",
          "name":"demo",
          "time":"2022-05-08T18:22:05.190Z",
          "version":"0.0.1-SNAPSHOT",
          "group":"com.sanjuthomas"
       }
    }
```

