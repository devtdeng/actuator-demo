# Spring Boot Actuator
[Spring Boot Actuator: Production-ready features](https://docs.spring.io/spring-boot/docs/current/reference/html/production-ready-endpoints.html#production-ready-endpoints-exposing-endpoints), more endpoints like /acutator/heapdump in Spring Boot 2.x. 
# Create Actuator Demo
## Create spring-boot app with Actuator, Web enabled.
1. Access https://start.spring.io, "Search for dependencies" to find *Actuator*, *Web* and select it. Set *Artifact* to "actuator-demo", download and unzip file. 
3. Confirm *spring-boot-starter-actuator* and *spring-boot-starter-web* are included in both pom.xml file. 
```
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-actuator</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>
```
## Run demo on local with default settings
1. *mvn spring-boot:run*
2. *curl http://localhost:8080/actuator*, only 3 endpoints available. 
*{"_links":{"self":{"href":"http://localhost:8080/actuator","templated":false},"health":{"href":"http://localhost:8080/actuator/health","templated":false},"info":{"href":"http://localhost:8080/actuator/info","templated":false}}}*
3. *curl http://localhost:8080/actuator/health*
*{"status":"UP"}*

## Enable more endpoints
1. Edit applicatin.properties to include all endpoints.
```
management.endpoints.web.exposure.include=*
```
2. *mvn spring-boot:run*
3. *curl http://localhost:8080/actuator*, more endpoints available.
*{"_links":{"self":{"href":"http://localhost:8080/actuator","templated":false},"auditevents":{"href":"http://localhost:8080/actuator/auditevents","templated":false},"beans":{"href":"http://localhost:8080/actuator/beans","templated":false},"health":{"href":"http://localhost:8080/actuator/health","templated":false},"conditions":{"href":"http://localhost:8080/actuator/conditions","templated":false},"configprops":{"href":"http://localhost:8080/actuator/configprops","templated":false},"env":{"href":"http://localhost:8080/actuator/env","templated":false},"env-toMatch":{"href":"http://localhost:8080/actuator/env/{toMatch}","templated":true},"info":{"href":"http://localhost:8080/actuator/info","templated":false},"loggers":{"href":"http://localhost:8080/actuator/loggers","templated":false},"loggers-name":{"href":"http://localhost:8080/actuator/loggers/{name}","templated":true},"heapdump":{"href":"http://localhost:8080/actuator/heapdump","templated":false},"threaddump":{"href":"http://localhost:8080/actuator/threaddump","templated":false},"metrics-requiredMetricName":{"href":"http://localhost:8080/actuator/metrics/{requiredMetricName}","templated":true},"metrics":{"href":"http://localhost:8080/actuator/metrics","templated":false},"scheduledtasks":{"href":"http://localhost:8080/actuator/scheduledtasks","templated":false},"httptrace":{"href":"http://localhost:8080/actuator/httptrace","templated":false},"mappings":{"href":"http://localhost:8080/actuator/mappings","templated":false}}}*
4. Access threaddump or heapdump endpoints from browser, dump will be downloded.
## Push to Cloud Foundry
1. *mvn package -Dmaven.test.skip && cf push actuator-demo -p target/actuatordemo-0.0.1-SNAPSHOT.jar* 
2. *curl https://actuator-demo.APP_DOMAIN/actuator*
*{"_links":{"self":{"href":"https://actuator-demo.APP_DOMAIN/actuator","templated":false},"auditevents":{"href":"https://actuator-demo.APP_DOMAIN/actuator/auditevents","templated":false},"beans":{"href":"https://actuator-demo.APP_DOMAIN/actuator/beans","templated":false},"health":{"href":"https://actuator-demo.APP_DOMAIN/actuator/health","templated":false},"conditions":{"href":"https://actuator-demo.APP_DOMAIN/actuator/conditions","templated":false},"configprops":{"href":"https://actuator-demo.APP_DOMAIN/actuator/configprops","templated":false},"env-toMatch":{"href":"https://actuator-demo.APP_DOMAIN/actuator/env/{toMatch}","templated":true},"env":{"href":"https://actuator-demo.APP_DOMAIN/actuator/env","templated":false},"info":{"href":"https://actuator-demo.APP_DOMAIN/actuator/info","templated":false},"loggers":{"href":"https://actuator-demo.APP_DOMAIN/actuator/loggers","templated":false},"loggers-name":{"href":"https://actuator-demo.APP_DOMAIN/actuator/loggers/{name}","templated":true},"heapdump":{"href":"https://actuator-demo.APP_DOMAIN/actuator/heapdump","templated":false},"threaddump":{"href":"https://actuator-demo.APP_DOMAIN/actuator/threaddump","templated":false},"metrics":{"href":"https://actuator-demo.APP_DOMAIN/actuator/metrics","templated":false},"metrics-requiredMetricName":{"href":"https://actuator-demo.APP_DOMAIN/actuator/metrics/{requiredMetricName}","templated":true},"scheduledtasks":{"href":"https://actuator-demo.APP_DOMAIN/actuator/scheduledtasks","templated":false},"httptrace":{"href":"https://actuator-demo.APP_DOMAIN/actuator/httptrace","templated":false},"mappings":{"href":"https://actuator-demo.APP_DOMAIN/actuator/mappings","templated":false}}}*
3. Access any of above endpoints, such as threadump at https://actuator-demo.APP_DOMAIN/actuator/threaddump