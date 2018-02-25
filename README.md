# DBstudy
## mysql和oracle的区别
> 1.整体来说：oracle属于大型数据库，对并发和联机事务处理（OLTP）等唯一都要比mysql好很多，而mysql属于中小型数据库，在操作上更简单。

> 2.从建库来说，一个oracle服务只能有一个库，而mysql一个服务下可存在多个库。

> 3.从建表来说：mysql主键一般使用自增使用auto increment即可，而oracle虽然没有自增，但可配置多种增量方式。

> 4.操作来说：

  *  mysql日期： 可以通过字符串直接转化，而oracle必须要通过format为date格式才可以存储。
  *  引号：mysql可以使用单双引号，而oracle只能使用单引号。
  *  空字符串的处理：mysql可以拥有没有内容的字符串，而oracle只能不允许这样
  *  分页的处理，mysql使用limit就可以完成分页，而oracle必须要完成分页就对多次处理结果集。
