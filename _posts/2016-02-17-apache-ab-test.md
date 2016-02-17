---
layout: post
title:  "Apache Benche ab 测试."
category:ab 测试
tags:  压力测试 ab benche 请求.
---

##Apache Benche

### 简介


###单独安装

1、使用yum 安装

```
yum install httpd-tools

```

2、独立编译安装
	独立安装apache benche 需要的源码包：
	ab-standalone-0.1.tar.bz2--->https://code.google.com/archive/p/apachebench-standalone/downloads
	apr-1.5.2.tar.gz
	apr-util-1.5.4.tar.gz
	
	2.1 安装apr
		tar -zxvf apr-1.5.2.tar.gz
		cd apr-1.5.2 
		./configure
		make & make install
		ln -s /usr/local/apr/lib/pkgconfig/apr-1.pc /usr/local/lib/pkgconfig/apr-1.pc
		tar -jxvf ab-standalone-0.1.tar.bz2
		cd ab-standalone-0.1
		make apr-skeletion(如果缺少环境变量直接配置profile 指向apr 的目录即可)
		tar -zxvf apr-util-1.5.4.tar.gz
		cd apr-util-1.5.4
		./configure --with-apr=/usr/local/apr
		make & make install
		cd ab-standalone-0.1
		vim ab
		
		
		
		```
	
		 /* catch legitimate fatal apr_socket_recv errors */
        else if (status != APR_SUCCESS) {
            err_recv++;
            if (recverrok) {
                bad++;
                close_connection(c);
                if (verbosity >= 1) {
                    char buf[120];
                    fprintf(stderr,"%s: %s (%d)\n", "apr_socket_recv", apr_strerror(status, buf, sizeof buf), 				status);
                }
                return;
            } else {
            /**	修改第1380行下面的错误打印：**/
                bad++;
                close_connection(c);
                /**apr_err("apr_socket_recv", status);*/
            }
        }
		```
		
		修改宏定义的20000 限制大小
		
		
		执行 make ab 
		
		测试:./ab -c30000 -n30000 http://127.0.0.1/
		
	2.2 ab 使用参数介绍
	
	
	
	
	
		
		
		
		
		
	






