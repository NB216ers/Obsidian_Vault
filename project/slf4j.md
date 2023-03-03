## Java 世界中的日志框架
| 名称     | Jar 包                                 | 描述                                                  |
| -------- | -------------------------------------- | ----------------------------------------------------- |
| slf4j    | slf4j-api. Jar                         | 门面日志框架                                          |
| jcl      | commons-logging. Jar                   | 门面日志框架（很久没更新）                            |
| log4j    | log4j. Jar                             | log4j 1. X , 底层日志框架 （已经不在更新维护）                            |
| reload4j | reload4j. Jar                          | log4j 1. X 的分叉版本，并修复了安全漏洞，底层日志框架 |
| log4j2   | log4j-api. Jar, log4j-core. Jar        | log4j 2. X, 底层日志框架                              |
| jul      | JDK                                    | 底层日志框架                                          |
| logback  | logback-classic. Jar logback-core. Jar | 底层日志框架                                                      |

## 门面日志框架
### 什么是门面日志框架
提供日志接口，不提供日志系统的具体实现。


使用 **适配层** 将**门面日志框架**和**底层日志框架**绑定起来。