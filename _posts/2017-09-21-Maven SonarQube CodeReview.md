---
layout:     post
title:      CodeReview 
subtitle:    "\"Maven SonarQube CodeReview\""
date:       2017-09-21
author:     mrchang
header-img: img/post-bg-re-vs-ng2.jpg
catalog: true
tags:
    - Maven
    - SonarQube
    - CodeReview

---


## 介绍

1. SonarQube
	
	* 官网： https://www.sonarqube.org/
	* 介绍：（曾用名Sonar（声纳）是一个开源的代码质量管理系统。 

2. SonarQube 特征

	* 支持超过25种编程语言：Java、C/C++、C#、PHP、Flex、Groovy、JavaScript、Python、PL/SQL、COBOL等。（不过有些是商业软件插件）
	* 可以在Android开发中使用
	* 提供重复代码、编码标准、单元测试、代码覆盖率、代码复杂度、潜在Bug、注释和软件设计报告
	* 提供了指标历史记录、计划图（“时间机器”）和微分查看
	* 提供了完全自动化的分析：与Maven、Ant、Gradle和持续集成工具（Atlassian Bamboo、Jenkins、Hudson等）* 与Eclipse开发环境集成
	* 与JIRA、Mantis、LDAP、Fortify等外部工具集
	* 支持扩展插件
	* 利用SQALE计算技术债务
	* 支持Tomcat。不过计划从SonarQube 4.1起终止对Tomcat的支持。


## 安装

1. 依然使用docker image 部署

2. 如果没有安装docker [请参考这篇博客](https://jetbrains.org.cn/2017/09/13/maven%E7%A7%81%E6%9C%8D-nexus/)

3. 启动

		docker run -d --name sonarqube \
	    -p 9000:9000 -p 9092:9092 \
	    -e SONARQUBE_JDBC_USERNAME=sonar \
	    -e SONARQUBE_JDBC_PASSWORD=sonar \
	    -e SONARQUBE_JDBC_URL=jdbc:mysql://192.168.199.131:3306/tryspread?useUnicode=true&characterEncoding=utf-8 \
	    sonarqube
	    
4. 访问。http://ip:9000

	![](http://ovwa7dn9w.bkt.clouddn.com/17-9-21/39675683.jpg)

## 项目中使用
1. maven setting.xml 设置
		![](http://ovwa7dn9w.bkt.clouddn.com/17-9-21/60017734.jpg)
		
		
2.  pom添加插件
		
		<plugin>
                <groupId>org.sonarsource.scanner.maven</groupId>
                <artifactId>sonar-maven-plugin</artifactId>
                <version>3.3.0.603</version>
        </plugin>
	
3. 使用。执行 mvn sonar:sonar 即可

4. 观察
	
	![](http://ovwa7dn9w.bkt.clouddn.com/17-9-21/98104526.jpg)
	
5. 关于SonarQube详细设置，下个博客在讲。




