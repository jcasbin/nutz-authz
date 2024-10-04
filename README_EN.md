# jcasbin-nutz-plugin
[![build](https://github.com/jcasbin/jcasbin-nutz-plugin/actions/workflows/maven-ci.yml/badge.svg)](https://github.com/jcasbin/jcasbin-nutz-plugin/actions/workflows/maven-ci.yml)
[![Maven Central](https://img.shields.io/maven-central/v/org.casbin/jcasbin-nutz-plugin.svg)](https://central.sonatype.com/artifact/org.casbin/jcasbin-nutz-plugin)

jcasbin-nutz-plugin is an authorization middleware for [Nutz](https://nutzam.com/), it's based on [https://github.com/casbin/jcasbin](https://github.com/casbin/jcasbin). It is developed under the latest Nutz ``1.r.65`` and Java ``8``.

## Installation

```xml
<dependency>
    <groupId>org.casbin</groupId>
    <artifactId>jcasbin-nutz-plugin</artifactId>
    <version>1.0.0</version>
</dependency>
```

## Simple Example

This project itself is a working Nutz project that integrates with jCasbin. The steps to use jCasbin in your own Nutz project are:

1. Copy the [JCasbinAuthzFilter](https://github.com/jcasbin/jcasbin-nutz-plugin/blob/master/src/main/java/org/jcasbin/plugins/JCasbinAuthzFilter.java) class to your own project.
2. Copy [authz_model.conf](https://github.com/jcasbin/jcasbin-nutz-plugin/blob/master/examples/authz_model.conf) and [authz_policy.csv](https://github.com/jcasbin/jcasbin-nutz-plugin/blob/master/examples/authz_policy.csv) to your project. You can modify them to your own jCasbin model and policy (or loading policy from DB), see [Model persistence](https://github.com/casbin/casbin/wiki/Model-persistence) and [Policy persistence](https://github.com/casbin/casbin/wiki/Policy-persistence).
3. Replace the [HttpBasicAuthnFilter](https://github.com/jcasbin/jcasbin-nutz-plugin/blob/master/src/main/java/org/jcasbin/plugins/HttpBasicAuthnFilter.java) class (which provides [HTTP basic authentication](https://en.wikipedia.org/wiki/Basic_access_authentication)) with your own authentication like OAuth, Apache Shiro, Spring Security, etc. Rewrite ``JCasbinAuthzFilter``'s [String getUser(HttpServletRequest request)](https://github.com/jcasbin/jcasbin-nutz-plugin/blob/master/src/main/java/org/jcasbin/plugins/JCasbinAuthzFilter.java#L42-L56) method to make sure jCasbin can get the authenticated user name.
4. Make sure the ``JCasbinAuthzFilter`` filter is loaded, so it can filter all your requests. To do this, you can use the following code in your ``MainModule`` class:

```java
@Filters({@By(type=JCasbinAuthzFilter.class), @By(type=HttpBasicAuthnFilter.class)})
public class MainModule {
    ...
}
```

## Tutorials

- [比Shiro更简单的Nutz权限管理：与jCasbin权限管理框架进行整合](https://nutz.cn/yvr/t/7v1m8jh2qejo7qu5460m2qgmul)

## Getting Help

- [jCasbin](https://github.com/casbin/jcasbin)

## License

This project is under Apache 2.0 License. See the [LICENSE](LICENSE) file for the full license text.
