# mysql中varchar类型的id，where id=1，会用到索引吗？int 类型的id，where id="1"，会用到索引吗？为什么？

对于int类型id，查询的varchar 类型 ‘1’会隐式转换成 1，‘1’和 1都能正常走索引；
对于varchar类型id，查询的int 类型 1不会转换，‘1’正常走索引，1走全表；