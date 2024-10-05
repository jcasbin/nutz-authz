# jcasbin-nutz-plugin
[![build](https://github.com/jcasbin/jcasbin-nutz-plugin/actions/workflows/maven-ci.yml/badge.svg)](https://github.com/jcasbin/jcasbin-nutz-plugin/actions/workflows/maven-ci.yml)
[![Maven Central](https://img.shields.io/maven-central/v/org.casbin/jcasbin-nutz-plugin.svg)](https://central.sonatype.com/artifact/org.casbin/jcasbin-nutz-plugin)

[(For English version)](https://github.com/jcasbin/jcasbin-nutz-plugin/blob/master/README_EN.md)

jcasbin-nutz-plugin是专门为Java Web框架[Nutz](https://nutzam.com/)打造的权限管理插件, 基于[https://github.com/casbin/jcasbin](https://github.com/casbin/jcasbin)技术实现。基于最新的Nutz ``1.r.65``和Java ``8``版本进行开发。

## 安装

```xml
<dependency>
    <groupId>org.casbin</groupId>
    <artifactId>jcasbin-nutz-plugin</artifactId>
    <version>1.0.0</version>
</dependency>
```

## 一个简单例子

本项目自身就是一个Nutz项目，演示了如何与jCasbin权限框架集成。如果你要在自己的Nutz项目里使用jCasbin进行权限管理，可以参考如下步骤：

1. 把这个类：[JCasbinAuthzFilter](https://github.com/jcasbin/jcasbin-nutz-plugin/blob/master/src/main/java/org/jcasbin/plugins/JCasbinAuthzFilter.java)复制到你自己的项目里；
2. 把jCasbin的模型文件：[authz_model.conf](https://github.com/jcasbin/jcasbin-nutz-plugin/blob/master/examples/authz_model.conf)和策略文件：[authz_policy.csv](https://github.com/jcasbin/jcasbin-nutz-plugin/blob/master/examples/authz_policy.csv)复制到你自己的项目里。你可以按自己需求这几个文件（或者直接从数据库读取策略），详情请参考：[如何读写jCasbin模型](https://github.com/casbin/casbin/wiki/Model-persistence)以及[如何读写jCasbin策略](https://github.com/casbin/casbin/wiki/Policy-persistence)；
3. 把这个类：[HttpBasicAuthnFilter](https://github.com/jcasbin/jcasbin-nutz-plugin/blob/master/src/main/java/org/jcasbin/plugins/HttpBasicAuthnFilter.java)（实现了[HTTP basic authentication](https://en.wikipedia.org/wiki/Basic_access_authentication)）替换成你自己的身份认证机制（用户登录），比如OAuth、Apache Shiro、Spring Security等。重写``JCasbinAuthzFilter``里的这个方法：[String getUser(HttpServletRequest request)](https://github.com/jcasbin/jcasbin-nutz-plugin/blob/master/src/main/java/org/jcasbin/plugins/JCasbinAuthzFilter.java#L42-L56)来保证jCasbin能够得到登录后的用户名；
4. 保证``JCasbinAuthzFilter``过滤器被加载, 使其可以过滤所有请求。可以参考下面的例子对``MainModule``类进行修改：

```java
@Filters({@By(type=JCasbinAuthzFilter.class), @By(type=HttpBasicAuthnFilter.class)})
public class MainModule {
    ...
}
```

## 教程

- [比Shiro更简单的Nutz权限管理：与jCasbin权限管理框架进行整合](https://nutz.cn/yvr/t/7v1m8jh2qejo7qu5460m2qgmul)

## 帮助

- [jCasbin](https://github.com/casbin/jcasbin)

## 协议

本软件采用``Apache 2.0``授权协议开源，请点击[LICENSE](LICENSE)查看完整授权协议。
