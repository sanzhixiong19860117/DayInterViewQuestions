# 索引不适用的条件

1. 索引列上有函数。
2. 不满足最左前缀。
3. 使用了不等号。
4. 使用了范围查询。

1. 唯一性太差的字段不适合单独创建索引，即使频繁作为查询条件。

2. 更新非常频繁的字段不适合创建索引。

3. 不会出现在 WHERE 子句中的字段不该创建索引。

4. 表记录太少。

   

   sql优化，有点沾边。如下：
   福哥口诀法：尽最不范覆 不囊来字哦       （sql优化：尽量全值匹配、最佳左前缀法则、不在索引列上做任何操作、范围条件放最后、覆盖索引尽量用、
     不等于要甚用、Null/Not 有影响、Like查询要当心、字符类型加引号、OR改UNION效率高）