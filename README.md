[![Maven Central](https://maven-badges.herokuapp.com/maven-central/com.github.sabomichal/jooq-meta-postgres-flyway/badge.svg)](https://maven-badges.herokuapp.com/maven-central/com.github.sabomichal/jooq-meta-postgres-flyway) ![Java CI with Maven](https://github.com/sabomichal/jooq-meta-postgres-flyway/workflows/Java%20CI%20with%20Maven/badge.svg)
# jooq-meta-postgres-flyway
#### the jOOQ PostgreSQL DDL database with Flyway migrations
This package provides a jOOQ meta data source that spins up a PostgreSQL databse running inside docker container using Testcontainers, migrates the database schema using Flyway before reverse engineering the outcome by jOOQ code generator.

## Usage
### Maven
Simply add the meta plugin as a dependency to jOOQ codegen maven plugin. The following example demonstrates the usage.
```xml
<plugin>
    <groupId>org.jooq</groupId>
    <artifactId>jooq-codegen-maven</artifactId>
    <dependencies>
        <dependency>
            <groupId>com.github.sabomichal</groupId>
            <artifactId>jooq-meta-postgres-flyway</artifactId>
            <version>1.0.4</version>
        </dependency>
    </dependencies>
    <executions>
        <execution>
            <id>jooq-codegen</id>
            <phase>generate-sources</phase>
            <goals>
                <goal>generate</goal>
            </goals>
            <configuration>
                <generator>
                    <database>
                        <name>com.github.sabomichal.jooq.PostgresDDLDatabase</name>
                        <properties>
                            <property>
                                <key>locations</key>
                                <value>src/main/resources/db/migration</value>
                            </property>
                        </properties>
                        <includes>public.*</includes>
                        <excludes>flyway_schema_history</excludes>
                        <inputSchema>public</inputSchema>
                    </database>
                    <generate>
                        ...
                    </generate>
                </generator>
            </configuration>
        </execution>
    </executions>
</plugin>
```
If you like it, give it a star, if you don't, write an issue.
