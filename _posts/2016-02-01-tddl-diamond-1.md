---
layout: post
title:  "Diamond."
category: 分库分表
tags:  tddl diamond 分库 分表.
---

##Diamond

### 简介
引自：http://gao-xianglong.iteye.com/blog/2019729/

使用任何一种框架都需要配置一些配置源信息，毕竟每一种框架都有自己的规范，使用者务必遵守这些规范来实现自己的业务与基础框架的整合。
自然TDDL也不例外，也是有配置信息需要显式的进行配置，在TDDL中，配置可以基于2种方式，一种是基于本地配置文件的形式，另外一种则是基于Diamond的形式进行配置，在实际开发过程中，由于考虑到配置信息的集中管理所带来的好处，大部分开发人员愿意选择将TDDL的配置信息托管给Diamond，所以本文还是以Diamond作为TDDL的配置源。diamond是淘宝内部使用的一个管理持久配置的系统，它的特点是简单、可靠、易用，目前淘宝内部绝大多数系统的配置，由diamond来进行统一管理。diamond为应用系统提供了获取配置的服务，应用不仅可以在启动时从diamond获取相关的配置，而且可以在运行中对配置数据的变化进行感知并获取变化后的配置数据。

###安装


1、svn地址：http://code.taobao.org/svn/diamond

2、diamond 下载下来后diamond-sdk 报错，需要调整jdk编译版本到1.7以上

3、diamod 数据库脚本

```javascript


CREATE DATABASE diamond;
USE diamod;

CREATE TABLE config_info (
`id` BIGINT(64) UNSIGNED NOT NULL AUTO_INCREMENT,
`data_id` VARCHAR(255) NOT NULL DEFAULT '',
`group_id` VARCHAR(128) NOT NULL DEFAULT '',
`content` LONGTEXT NOT NULL,
`md5` VARCHAR(32) NOT NULL DEFAULT '',
`gmt_create` DATETIME NOT NULL DEFAULT '2010-05-05 00:00:00',
`gmt_modified` DATETIME NOT NULL DEFAULT '2010-05-05 00:00:00',
PRIMARY KEY  (`id`),
UNIQUE KEY `uk_config_datagroup` (`data_id`,`group_id`));

```

4、修改diamond jdbc.properties 文件得jdbc 配置为你的数据库

5、tomcat 容器发布diamond-server 并启动

6、启动后在浏览器访问：http://localhost:8080/diamond-server

7、如果查询时出现如下异常说明你的数据库版本超过了5.5所以需要升级jdbc驱动
升级后的jdbc驱动为：	

```java

			<dependency>
				<groupId>mysql</groupId>
				<artifactId>mysql-connector-java</artifactId>
				<version>5.1.37</version>
			</dependency>

```

启动后的查询异常:

```java

com.mysql.jdbc.exceptions.jdbc4.MySQLSyntaxErrorException: You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'OPTION SQL_SELECT_LIMIT=10000' at line 1
	at sun.reflect.NativeConstructorAccessorImpl.newInstance0(Native Method)
	at sun.reflect.NativeConstructorAccessorImpl.newInstance(NativeConstructorAccessorImpl.java:57)
	at sun.reflect.DelegatingConstructorAccessorImpl.newInstance(DelegatingConstructorAccessorImpl.java:45)
	at java.lang.reflect.Constructor.newInstance(Constructor.java:526)
	at com.mysql.jdbc.Util.handleNewInstance(Util.java:406)
	at com.mysql.jdbc.Util.getInstance(Util.java:381)
	at com.mysql.jdbc.SQLError.createSQLException(SQLError.java:1031)
	at com.mysql.jdbc.SQLError.createSQLException(SQLError.java:957)
	at com.mysql.jdbc.MysqlIO.checkErrorPacket(MysqlIO.java:3376)
	at com.mysql.jdbc.MysqlIO.checkErrorPacket(MysqlIO.java:3308)
	at com.mysql.jdbc.MysqlIO.sendCommand(MysqlIO.java:1837)
	at com.mysql.jdbc.MysqlIO.sqlQueryDirect(MysqlIO.java:1961)
	at com.mysql.jdbc.ConnectionImpl.execSQL(ConnectionImpl.java:2537)
	at com.mysql.jdbc.StatementImpl.executeSimpleNonQuery(StatementImpl.java:1463)
	at com.mysql.jdbc.PreparedStatement.executeQuery(PreparedStatement.java:1875)
	at org.apache.commons.dbcp.DelegatingPreparedStatement.executeQuery(DelegatingPreparedStatement.java:93)
	at org.apache.commons.dbcp.DelegatingPreparedStatement.executeQuery(DelegatingPreparedStatement.java:93)
	at org.springframework.jdbc.core.JdbcTemplate$1.doInPreparedStatement(JdbcTemplate.java:644)
	at org.springframework.jdbc.core.JdbcTemplate.execute(JdbcTemplate.java:587)
	at org.springframework.jdbc.core.JdbcTemplate.query(JdbcTemplate.java:637)
	at org.springframework.jdbc.core.JdbcTemplate.query(JdbcTemplate.java:666)
	at org.springframework.jdbc.core.JdbcTemplate.query(JdbcTemplate.java:674)
	at org.springframework.jdbc.core.JdbcTemplate.queryForObject(JdbcTemplate.java:729)
	at org.springframework.jdbc.core.JdbcTemplate.queryForObject(JdbcTemplate.java:745)
	at org.springframework.jdbc.core.JdbcTemplate.queryForInt(JdbcTemplate.java:776)
	at com.taobao.diamond.server.utils.PaginationHelper.fetchPage(PaginationHelper.java:58)
	at com.taobao.diamond.server.service.PersistService.findAllConfigInfo(PersistService.java:195)
	at com.taobao.diamond.server.service.ConfigService.findConfigInfo(ConfigService.java:212)
	at com.taobao.diamond.server.controller.AdminController.listConfig(AdminController.java:223)
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:57)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:606)
	at org.springframework.web.bind.annotation.support.HandlerMethodInvoker.invokeHandlerMethod(HandlerMethodInvoker.java:176)
	at org.springframework.web.servlet.mvc.annotation.AnnotationMethodHandlerAdapter.invokeHandlerMethod(AnnotationMethodHandlerAdapter.java:436)
	at org.springframework.web.servlet.mvc.annotation.AnnotationMethodHandlerAdapter.handle(AnnotationMethodHandlerAdapter.java:424)
	at org.springframework.web.servlet.DispatcherServlet.doDispatch(DispatcherServlet.java:923)
	at org.springframework.web.servlet.DispatcherServlet.doService(DispatcherServlet.java:852)
	at org.springframework.web.servlet.FrameworkServlet.processRequest(FrameworkServlet.java:882)
	at org.springframework.web.servlet.FrameworkServlet.doGet(FrameworkServlet.java:778)
	at javax.servlet.http.HttpServlet.service(HttpServlet.java:622)
	at javax.servlet.http.HttpServlet.service(HttpServlet.java:729)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:291)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:206)
	at org.apache.tomcat.websocket.server.WsFilter.doFilter(WsFilter.java:52)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:239)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:206)
	at com.taobao.diamond.server.listener.AuthorizationFilter.doFilter(AuthorizationFilter.java:50)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:239)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:206)
	at org.springframework.web.filter.CharacterEncodingFilter.doFilterInternal(CharacterEncodingFilter.java:88)
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:76)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:239)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:206)
	at org.apache.catalina.core.StandardWrapperValve.invoke(StandardWrapperValve.java:219)
	at org.apache.catalina.core.StandardContextValve.invoke(StandardContextValve.java:106)
	at org.apache.catalina.authenticator.AuthenticatorBase.invoke(AuthenticatorBase.java:502)
	at org.apache.catalina.core.StandardHostValve.invoke(StandardHostValve.java:142)
	at org.apache.catalina.valves.ErrorReportValve.invoke(ErrorReportValve.java:79)
	at org.apache.catalina.valves.AbstractAccessLogValve.invoke(AbstractAccessLogValve.java:617)
	at org.apache.catalina.core.StandardEngineValve.invoke(StandardEngineValve.java:88)
	at org.apache.catalina.connector.CoyoteAdapter.service(CoyoteAdapter.java:518)
	at org.apache.coyote.http11.AbstractHttp11Processor.process(AbstractHttp11Processor.java:1091)
	at org.apache.coyote.AbstractProtocol$AbstractConnectionHandler.process(AbstractProtocol.java:668)
	at org.apache.tomcat.util.net.NioEndpoint$SocketProcessor.doRun(NioEndpoint.java:1527)
	at org.apache.tomcat.util.net.NioEndpoint$SocketProcessor.run(NioEndpoint.java:1484)
	at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1145)
	at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:615)
	at org.apache.tomcat.util.threads.TaskThread$WrappingRunnable.run(TaskThread.java:61)
	at java.lang.Thread.run(Thread.java:745)


```










