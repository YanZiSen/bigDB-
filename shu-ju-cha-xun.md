* 数据查询

在sql输入栏输入对应的语句可进实现对数据表的增删改查等动能，sql输入区支持输入多条语句进行操作；多条语句应以分号结尾；输入语句后点击执行即可。执行完毕后会显示每一条语句的执行时间和执行结果。如图

![](/assets/执行结果.png)语句执行失败后有相关的提示如下图![](/assets/错误信息.png)

* sql语句支持

  * 兼容SQL92标准，支持对单条/批量记录的增删改查，可对海量数据灵活的进行多维分析、数据透视、数据筛选、数据定义等。

  * 支持简单的SQL语句：select、update、drop、delete等

  * 支持复杂的SQL语句：JOIN、HAVING、DISTINCT等。

  * 支持带函数的SQL语句：avg\(\)、sum\(\)、max\(\)、min\(\)等。

  * 支持对任意字段进行组合查询。

  * 支持5条语句同时检索。
  
  * 特殊字符需要转义，具体详情参考impala 英文文档：https://impala.apache.org/docs/build/html/topics/impala_literals.html
