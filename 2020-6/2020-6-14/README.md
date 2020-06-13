# Redis底层数据结构？

- SDS simple synamic string：简单动态字符串。支持自动动态扩容的字节数组 。
- list ：链表 。双端链表。
- dict ：字典。使用双哈希表实现的, 支持平滑扩容的字典 。
- zskiplist ：跳跃表。附加了后向指针的跳跃表 。
- intset ： 整数集合。用于存储整数数值集合的自有结构 。
- ziplist ：压缩列表。一种实现上类似于TLV, 但比TLV复杂的, 用于存储任意数据的有序序列的数据结构 。
- quicklist：快速列表。一种以ziplist作为结点的双链表结构, 实现的非常不错 。
- zipmap ： 压缩字典。一种用于在小规模场合使用的轻量级字典结构 。
- String底层是SDS 内部编码 int，emstr，raw 。
- hash是ziplist与hashtable 。
- list采取的双端链表linklist，压缩列表ziplist。
- set是hashtable和inset 。
- zset是ziplist和skiplist。