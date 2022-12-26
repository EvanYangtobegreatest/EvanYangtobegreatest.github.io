---
title: vue+springboot前后端分离结合easyexcel实现excel导入导出功能
date: 2022-09-05 14:59:48
tags:
---

## 使用easyexcel实现excel导入导出功能

基于springboot，前端使用vue，使用阿里的easyexcel实现了单sheet表导入导出，多sheet表导入导出，单数据库表导入导出，多数据库表导入导出。

**首先需要搭建好spingboot和前端开发项目环境**

然后就可以开始开发excel导入导出功能

**首先需要引入easyexcel的maven依赖**

```xml
<!--在pom.xml文件添加以下依赖  -->
 <!--阿里easyexcel 用于进行Excel处理 -->
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>easyexcel</artifactId>
            <version>2.2.10</version>
        </dependency>
```

**根据自己需要的excel表作为对象，建立一个实体类**

有几个注解是重点

```java
//按照数据库表定义好实体类，为其加上注解 @ExcelProperty(value = "xxx", index = 0) ，其中value值对应的是excel表的表头，index的值为数字，代表该列在excel表里面的位置，数字越小列越靠前
// @ExcelIgnore 使用这个注解可以在生成excel时不显示该字段
// @ColumnWidth(20) 自定义列宽
public class User {
    // 主键id
    @ExcelIgnore // 生成报表时忽略，不生成次字段
    private Integer id;
    @ExcelProperty(value = "姓名", index = 0) // 定义表头名称和位置,0代表第一列
    private String name;
    @ExcelProperty(value = "性别", index = 1)
    private String sex;
    @ExcelProperty(value = "年龄", index = 2)
    private Integer age;
    //@ColumnWidth(20) // 定义列宽,使用自适应列宽则注释，不使用则可靠此注解自定义
    @DateTimeFormat(value = "yyyy-MM-dd")
    @ExcelProperty(value = "出生日期", index = 3)
    private String birthday;
}

```

