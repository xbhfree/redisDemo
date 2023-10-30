# redis简介

* remote dictionary server(远程字典服务)
* ansic语言编写，遵守BSD协议

## resdis应用场景

缓存加速、分布式会话、排行榜场景、分布式计数器、分布式锁

## reids安装

* 官网：www.redis.io 下载解压即可
* 虚拟机部署
  1. https://blog.csdn.net/qq_38584262/article/details/125773286

## redis7新特性

* redis functions
* client-eviction
* multi-part aof
* acl v2
* 新增50个命令
* listpack替代ziplist
* 底层性能提升

# redis基础

## 十大基础类型

1. String  字符串

   * 是二进制安全的，可以包含jpg图片或者序列化的对象
   * 字符串value最大是512M

2. Bitmap  位图

   * 1 byte = 8 bit
   * 位图就是由0、1组成的二进制数组

3. Bitfield  位域

   * 作用：一次性操作多个bit位域（连续的多个bit位），执行一系列操作返回一个响应数组，这个数组中的元素对应参数列表中相应操作的执行结果

4. Hash  哈希表

   * String类型的filed（字段），和value（值）的映射表，适合存储对象
   * 最多可以包含2^32-1个元素，每个哈希表可以包含超过40亿的元素

5. List  列表

   * 字符串列表，底层为双端列表
   * 最多可以包含2^32-1个元素，每个列表可以包含超过40亿的元素

6. Set  集合

   * String类型的无序集合，不能出现重复数据
   * 集合对象的编码可以是intset或者hashtable
   * 底层通过hash表实现，添加删除复杂度为O（1）
   * 最多可以包含2^32-1个元素

7. Sorted Set（Z Set）有序集合

   * 每个元素会关联一个double类型的分数，redis通过分数为集合成员按从小到大排序
   * 不允许重复数据
   * zset成员唯一，但分数（score）可重复
   * 底层通过hash表实现，添加删除复杂度为O（1）
   * 最多可以包含2^32-1个元素

8. Geospatial  地理空间

   * 作用：存储地理位置信息，添加获取地理位置的坐标，可以计算不同位置之间的距离，根据经纬坐标获取指定范围内的地理位置集合

9. Hyperlog  基数统计

   * 作用：基数统计

   * 优点：输入元素的数量或者体积非常大时，计算基数所需的空间总是固定且很小的，每个hyperlog键只需要花费12kb内存，就可以计算接近2^64个不同元素的基数，这和元素越多耗费内存就越多的集合形成鲜明对比
   * 缺点：只会根据输入元素计算基数，不会储存输入元素本身，无法像set一样返回输入的各个元素

10. Stream  流

    * 作用：消息队列

## redis命令

1. 官网英文：https://redis.io/commands
2. 中文:http://www.redis.cn/commands.html

* 常用命令：
  1. get key             获取值
  2. set key value    设置值
  3. del key              删除值
  4. unlink  key        异步删除值，仅仅将key从keyspace删除，真正的删除会在后续异步执行
  5. keys *               查询所有key
  6. exists key         判断key是否存在，存在返回1
  7. type key           判断值的类型
  8. ttl key               查看还有多少秒过期，-1永不过期，-2已过期
  9. expire key 秒    设置过期时间
  10. move key dbindex【0-15】将当前数据库的key移动到指定的数据库db中
  11. select dbindex 切换数据库【0-15】。默认为0
  12. dbsize              查看当前数据库的key数量
  13. flushdb             清空当前数据库
  14. flushall              清空所有数据库
