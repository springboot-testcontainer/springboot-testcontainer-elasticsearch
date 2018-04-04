springboot-testcontainer-elasticsearch
======================================

[![Maven Central](https://maven-badges.herokuapp.com/maven-central/com.avides.springboot.testcontainer/springboot-testcontainer-elasticsearch/badge.svg)](https://maven-badges.herokuapp.com/maven-central/com.avides.springboot.testcontainer/springboot-testcontainer-elasticsearch)
[![Codacy Badge](https://api.codacy.com/project/badge/Grade/xxx)](https://www.codacy.com/app/springboot-testcontainer/springboot-testcontainer-elasticsearch)
[![Coverage Status](https://coveralls.io/repos/springboot-testcontainer/springboot-testcontainer-elasticsearch/badge.svg)](https://coveralls.io/r/springboot-testcontainer/springboot-testcontainer-elasticsearch)
[![Build Status](https://travis-ci.org/springboot-testcontainer/springboot-testcontainer-elasticsearch.svg?branch=master)](https://travis-ci.org/springboot-testcontainer/springboot-testcontainer-elasticsearch)

### Dependency
```xml
<dependency>
	<groupId>com.avides.springboot.testcontainer</groupId>
	<artifactId>springboot-testcontainer-elasticsearch</artifactId>
	<version>0.1.0-RC3</version>
	<scope>test</scope>
</dependency>
```

### Configuration
Properties consumed (in `bootstrap.properties`):
- `embedded.container.elasticsearch.enabled` (default is `true`)
- `embedded.container.elasticsearch.startup-timeout` (default is `30`)
- `embedded.container.elasticsearch.docker-image` (default is `docker.elastic.co/elasticsearch/elasticsearch:5.6.8`)
- `embedded.container.elasticsearch.http-port` (default is `9200`)
- `embedded.container.elasticsearch.transport-host` (default is `9300`)

Properties provided (in `application-it.properties`):
- `embedded.container.elasticsearch.host`
- `embedded.container.elasticsearch.http-port`
- `embedded.container.elasticsearch.transport-port`

Example for minimal configuration in `application-it.properties`:
```
spring.data.elasticsearch.cluster-nodes=${embedded.container.elasticsearch.host}:${embedded.container.elasticsearch.transport-port}
spring.data.elasticsearch.properties.client.transport.ignore_cluster_name=true
```

## Logging
To reduce logging insert this into the logback-configuration:
```xml
<!-- Testcontainers -->
<logger name="com.github.dockerjava.jaxrs" level="WARN" />
<logger name="com.github.dockerjava.core.command" level="WARN" />
<logger name="org.apache.http" level="WARN" />
```

## Labels
The container exports multiple labels to analyze running testcontainers:
- `TESTCONTAINER_SERVICE=elasticsearch`
- `TESTCONTAINER_IMAGE=${embedded.container.elasticsearch.docker-image}`
- `TESTCONTAINER_STARTED=$currentTimestamp`
