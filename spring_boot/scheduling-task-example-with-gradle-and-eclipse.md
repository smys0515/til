# Scheduling task example with Gradle and Eclipse
You can create Spring Boot application executing scheduled tasks with Gradle and Eclipse by the following steps.

## Set up Gradle build script
`build.gradle`
```
buildscript {
  repositories {
    mavenCentral()
  }
  dependencies {
    classpath("org.springframework.boot:spring-boot-gradle-plugin:1.5.8.RELEASE")
  }
}

apply plugin: 'java'
apply plugin: 'eclipse'
apply plugin: 'org.springframework.boot'

jar {
  baseName = 'sb-scheduling-tasks'
  version =  '0.1.0'
}

repositories {
  mavenCentral()
}

sourceCompatibility = 1.8
targetCompatibility = 1.8

dependencies {
  compile("org.springframework.boot:spring-boot-starter")
  testCompile("junit:junit")
}
```

## Run Eclipse task
`gradle eclipse`

## Create scheduled tasks
`src/main/java/smys0515/tasks/scheduling/sb/ScheduledTasks.java`
```
@Component
public class ScheduledTasks {

    private static final Logger LOG = LoggerFactory.getLogger(ScheduledTasks.class);

    private static final SimpleDateFormat DATE_FORMAT = new SimpleDateFormat("HH:mm:ss");

    @Scheduled(cron = "*/10 * * * * *")
    public void reportCurrentTimeEveryTenSeconds() {
        LOG.info("The time is now {}", DATE_FORMAT.format(new Date()));
    }

    @Scheduled(cron = "*/30 * * * * *")
    public void reportCurrentTimeEveryThirtySeconds() {
        LOG.info("The time is now {}", DATE_FORMAT.format(new Date()));
    }

}
```

`src/main/java/smys0515/tasks/scheduling/sb/Application.java`
```
@EnableScheduling
@SpringBootApplication
public class Application {

    public static void main(String[] args) throws Exception {
        SpringApplication.run(Application.class);
    }
}
```

## Build application
`gradle build`

## Execute application
`java -jar build/libs/sb-scheduling-tasks-0.1.0.jar`

log
```
2017-11-26 01:15:10.001  INFO 15192 --- [pool-1-thread-1] s.tasks.scheduling.sb.ScheduledTasks     : The time is now 01:15:10
2017-11-26 01:15:20.001  INFO 15192 --- [pool-1-thread-1] s.tasks.scheduling.sb.ScheduledTasks     : The time is now 01:15:20
2017-11-26 01:15:30.001  INFO 15192 --- [pool-1-thread-1] s.tasks.scheduling.sb.ScheduledTasks     : The time is now 01:15:30
2017-11-26 01:15:30.001  INFO 15192 --- [pool-1-thread-1] s.tasks.scheduling.sb.ScheduledTasks     : The time is now 01:15:30
2017-11-26 01:15:40.001  INFO 15192 --- [pool-1-thread-1] s.tasks.scheduling.sb.ScheduledTasks     : The time is now 01:15:40
2017-11-26 01:15:50.001  INFO 15192 --- [pool-1-thread-1] s.tasks.scheduling.sb.ScheduledTasks     : The time is now 01:15:50
2017-11-26 01:16:00.001  INFO 15192 --- [pool-1-thread-1] s.tasks.scheduling.sb.ScheduledTasks     : The time is now 01:16:00
2017-11-26 01:16:00.001  INFO 15192 --- [pool-1-thread-1] s.tasks.scheduling.sb.ScheduledTasks     : The time is now 01:16:00
```

## See also
[Getting Started · Scheduling Tasks](https://spring.io/guides/gs/scheduling-tasks/)
