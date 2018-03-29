---
layout:     post
title:     	spring-cloud-config-server-git
subtitle:    "\"服务器为外部配置（名称值对或等效的YAML内容）提供了基于资源的HTTP。服务器可以使用@EnableConfigServer注释轻松嵌入到Spring Boot应用程序中。所以这个应用程序是一个配置服务器\""
date:       2018-04-05
author:     Mr Chang
header-img: img/post-bg-e2e-ux.jpg
catalog: true
tags:
    - spring cloud
    - spring-cloud-turbine
---


# Spring Cloud Config服务器


服务器为外部配置（名称值对或等效的YAML内容）提供了基于资源的HTTP。服务器可以使用@EnableConfigServer注释轻松嵌入到Spring Boot应用程序中。所以这个应用程序是一个配置服务器：


# 创建 Spring Cloud Config Server

1. 创建springboot工程，引入依赖

	    <parent>
	        <groupId>org.springframework.boot</groupId>
	        <artifactId>spring-boot-starter-parent</artifactId>
	        <version>1.5.10.RELEASE</version>
	        <relativePath/> <!-- lookup parent from repository -->
	    </parent>
	
	    <properties>
	        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
	        <project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
	        <java.version>1.8</java.version>
	        <spring-cloud.version>Dalston.SR4</spring-cloud.version>
	    </properties>
	
	    <dependencies>
	        <dependency>
	            <groupId>org.springframework.boot</groupId>
	            <artifactId>spring-boot-starter-actuator</artifactId>
	        </dependency>
	        <dependency>
	            <groupId>org.springframework.cloud</groupId>
	            <artifactId>spring-cloud-starter-bus-amqp</artifactId>
	        </dependency>
	        <dependency>
	            <groupId>org.springframework.cloud</groupId>
	            <artifactId>spring-cloud-config-server</artifactId>
	        </dependency>
	
	        <dependency>
	            <groupId>org.springframework.boot</groupId>
	            <artifactId>spring-boot-starter-test</artifactId>
	            <scope>test</scope>
	        </dependency>
	    </dependencies>
	
	    <dependencyManagement>
	        <dependencies>
	            <dependency>
	                <groupId>org.springframework.cloud</groupId>
	                <artifactId>spring-cloud-dependencies</artifactId>
	                <version>${spring-cloud.version}</version>
	                <type>pom</type>
	                <scope>import</scope>
	            </dependency>
	        </dependencies>
	    </dependencyManagement>
	    
	    
2. 启动类上写注解

		@SpringBootApplication
		@EnableConfigServer
		public class SpringCloudConfigServerGitApplication {
		
		    public static void main(String[] args) {
		        SpringApplication.run(SpringCloudConfigServerGitApplication.class, args);
		    }
		}
		
3. 修改application配置文件，添加配置
		
		spring.application.name=config-server
		spring.cloud.config.server.git.uri=https://github.com/changdaye/spring-cloud-config-repo-demo/
		server.port=8085
		logging.level.root=info
		spring.rabbitmq.host=118.24.24.243
		spring.rabbitmq.port=5672
		spring.rabbitmq.username=springcloud
		spring.rabbitmq.password=123456
		management.security.enabled=false
		
	* 这里我们直接是bus-mq版本的spring-cloud-config-server
	* 远程配置文件地址是 https://github.com/changdaye/spring-cloud-config-repo-demo

# 使用

1. 启动服务即可
2. 刷新配置命令 

		### 刷新my-initializr配置测试  ** 可以替换成端口号
		POST https://config-server-git.jetbrains.org.cn/bus/refresh?destination=my-initializr:**

# 公共config-server

* https://config-server-git.jetbrains.org.cn
* 远程配置中心位置：https://github.com/changdaye/spring-cloud-config-repo-demo，添加自己的配置只需要提交request合并即可。


# 参考资料

1. https://springcloud.cc/spring-cloud-dalston.html#_spring_cloud_config_server
2. https://github.com/changdaye/spring-cloud-config-repo-demo
3. https://github.com/changdaye/spring-cloud-study/tree/master/spring-cloud-config-server-git 



