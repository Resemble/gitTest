this project is to test git !
# README #

## 项目说明：
可乐二期项目，该项目主要是重构可乐一期项目，[后端地址]，[代码地址]
重构主要涉及：
1. controller 抽象
2. service 抽象
3. 引入 spring 进行生命周期管理
4. 使用 spring cache 进行缓存
5. 修改 login 
6. 加入 dev、test 和 product 三种环境配置
7. 修改 throw Exception 部分，详细抛出异常
8. 使用 enum 使得项目更加灵活
9. 使用 filter 对数据进行过滤
10. 加入 log

## 项目结构
```
├─filters                       # 环境打包 不同环境特有配置
│  ├─dev                        # 本地环境
│  │  └─properties              # 配置文件
│  ├─product                    # 生产环境
│  │  └─properties              
│  └─test                       # 测试环境
│      └─properties
├─groovy                        # 代码采用groovy语言
│  └─com
│      └─spiderdt
│          └─cocacola           # 可乐项目核心代码
│              ├─builder        # 抽象controller的hashmap重复部分，并引入具有请求池和timeout的AsyncHTTPBuilder
│              ├─controller     # 接受前端请求并将请求发送到service
│              ├─entity         # 各个controller对应一个entity来接受前端请求参数
│              ├─enums          # 密码更改的类型及状态进行枚举
│              ├─exception      # 将Exception具体化
│              ├─filter         # 过滤，cookie加入secure; HttpOnly，并过滤不符合格式的token
│              ├─handler        # 方便controller中数据处理
│              ├─service        # 抽象公共部分，CommonService处理category和HttpClientService处理所有数据获取，其余为各个controller对应请求
│              ├─utils          # 工具，sha加密、jsonConverter和密码验证
│              └─vo             # 具体对象，User用于接收登录post请求，ChangePasswordVo用于接收改变密码请求，Lockout用于缓存对象记录是否lock和登录失败次数
├─java                          # 未使用java
├─resources                     # 公共配置
│  ├─cache                      # 缓存配置
│  ├─messages                   # 动态更新配置，fixme未实现
│  ├─properties                 # 普通配置
│  └─spring                     # spring配置，使用注入方式，包括对context的注入，对bean的管理，加载缓存配置，验证码，校验器（未实现）
└─webapp                        # web
    └─WEB-INF                   # web配置
```

## 技术选型
+ 核心框架：[SpringMVC]
+ 缓存：[spring ehcache]
+ 打包工具：[gradle]
+ 开发语言：[groovy]

## 开发环境
| 软件 | 版本 |
| :---: | :----: |
| IntelliJ IDEA | 2017.1 |

## 项目依赖
| groupId | artifactId | version |
| :------: | :------: | :------: |
| spiderdt-adapter | spiderdt-adapter | 0.1.0-SNAPSHOT |
| org.spiderdt.groovy.modules.http-builder | http-builder | 0.7.3-SNAPSHOT |
| junit | junit | 4.12 |
| javax.servlet | javax.servlet-api | 3.0.1 |
| ch.qos.logback | logback-classic | 1.2.1 |
| org.logback-extensions | logback-ext-spring | 0.1.4 |
| org.slf4j | jcl-over-slf4j | 1.7.22 |
| net.sf.ehcache | ehcache | 2.10.3 |
| org.json | json | 20160810 |
| com.fasterxml.jackson.core | jackson-core | 2.8.2 |
| com.fasterxml.jackson.core | jackson-annotations | 2.5.1 |
| com.fasterxml.jackson.core | jackson-databind | 2.5.1 |
| org.springframework | spring-core | 4.3.4.RELEASE |
| org.springframework | spring-beans | 4.3.4.RELEASE |
| org.springframework | spring-context | 4.3.4.RELEASE |
| org.springframework | spring-context-support | 4.3.4.RELEASE |
| org.springframework | spring-expression | 4.3.4.RELEASE |
| org.springframework | spring-web | 4.3.4.RELEASE |
| org.springframework | spring-webmvc | 4.3.4.RELEASE |
| org.springframework | spring-test | 4.3.4.RELEASE |
| com.github.penggle | kaptcha | 2.3.2 |
| org.hibernate | hibernate-validator | 5.4.1.Final |
| org.glassfish | javax.el | 3.0.1-b08 |



## To Do List
+ [ ] 开发
    + [ ] common-cache
        + [ ] Redis
        + [ ] ehcache
        + [ ] memcached
    + [ ] http-service 重构
+ [ ] 持续集成，持续部署


## CHANGELOG 

See [CHANGELOG.md]



[CHANGELOG.md]: CHANGELOG.md
[后端地址]: https://cocacola.spiderdt.com/#/login
[代码地址]: https://bitbucket.org/spiderdata/cocacola-api-v2
[SpringMVC]: https://projects.spring.io/spring-framework/
[spring ehcache]: http://www.ehcache.org/
[gradle]: https://gradle.org/
[groovy]: http://groovy-lang.org/