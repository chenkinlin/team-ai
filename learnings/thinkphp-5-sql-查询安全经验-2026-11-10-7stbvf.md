---
title: ThinkPHP 5 SQL 查询安全经验
tags: [thinkphp, sql-injection, sql注入, 参数绑定, 白名单]
---

# ThinkPHP 5 SQL 查询安全经验

## 问题
在历史 PHP 项目中，直接将外部输入拼接进 SQL
可能导致 SQL 注入风险。

## 建议
优先使用项目当前 ThinkPHP 5.0.7 版本支持的
查询构造器和参数绑定。

对于无法使用参数绑定的排序字段、列名及表名，
必须使用服务端白名单。

## 适用范围
ThinkPHP 5.0.x 项目中的新增或修改查询。

## 限制
具体 API 写法须以项目安装的框架版本为准。
