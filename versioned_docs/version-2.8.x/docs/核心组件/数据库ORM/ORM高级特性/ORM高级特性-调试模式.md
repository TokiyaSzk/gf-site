---
slug: '/docs/core/gdb-senior-debugging'
title: 'ORM高级特性-调试模式'
sidebar_position: 2
hide_title: true
keywords: [GoFrame,GoFrame框架,ORM,调试模式,SQL,日志,数据库,配置示例,SetDebug,Debug配置]
description: '在GoFrame框架中使用ORM高级特性的调试模式。在开发阶段，通过Debug配置文件配置项或SetDebug配置方式，可以开启调试模式，使数据库SQL操作语句以DEBUG级别输出到终端或日志文件中，便于开发者进行问题排查和性能优化。'
---

为便于开发阶段调试， `GoFrame ORM` 支持调试模式，可以通过 `Debug` 配置文件配置项或者 `SetDebug` 配置方式开启调试模式， 随后任何的数据库 `SQL` 操作语句都将会由内置的日志对象，以 `DEBUG` 级别输出到终端或者日志文件中。以下是一个开启了调试模式的配置示例：

```yaml
database:
  default:
  - link:  "mysql:root:12345678@tcp(127.0.0.1:3306)/user"
    debug: true
```

输出的日志内容示例：

```html
2021-05-22 21:12:10.776 [DEBU] {38d45cbf2743db16f1062074f7473e5c} [  4 ms] [default] [rows:0  ] [txid:1] BEGIN
2021-05-22 21:12:10.776 [DEBU] {38d45cbf2743db16f1062074f7473e5c} [  0 ms] [default] [rows:0  ] [txid:1] SAVEPOINT `transaction0`
2021-05-22 21:12:10.789 [DEBU] {38d45cbf2743db16f1062074f7473e5c} [ 13 ms] [default] [rows:8  ] [txid:1] SHOW FULL COLUMNS FROM `user`
2021-05-22 21:12:10.790 [DEBU] {38d45cbf2743db16f1062074f7473e5c} [  1 ms] [default] [rows:1  ] [txid:1] INSERT INTO `user`(`id`,`name`) VALUES(1,'john')
2021-05-22 21:12:10.791 [DEBU] {38d45cbf2743db16f1062074f7473e5c} [  1 ms] [default] [rows:0  ] [txid:1] ROLLBACK TO SAVEPOINT `transaction0`
2021-05-22 21:12:10.791 [DEBU] {38d45cbf2743db16f1062074f7473e5c} [  0 ms] [default] [rows:1  ] [txid:1] INSERT INTO `user`(`id`,`name`) VALUES(2,'smith')
2021-05-22 21:12:10.792 [DEBU] {38d45cbf2743db16f1062074f7473e5c} [  1 ms] [default] [rows:0  ] [txid:1] COMMIT
```