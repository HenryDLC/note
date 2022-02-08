# Redis速查

### 键**(key)**

| keys *        | 查看当前库所有 key (匹配:keys *1)                            |
| ------------- | ------------------------------------------------------------ |
| exists key    | 判断某个 key 是否存在                                        |
| type key      | 查看你的 key 是什么类型                                      |
| del key       | 删除指定的 key 数据                                          |
| unlink key    | 根据 value 选择非阻塞删除,仅将 keys 从 keyspace 元数据中删除，真正的删除会在后续异步操作。 |
| expire key 10 | 10 秒钟:为给定的 key 设置过期时间                            |
| ttl key       | 查看还有多少秒过期，-1 表示永不过期，-2 表示已过期           |
| select        | 命令切换数据库                                               |
| dbsize        | 查看当前数据库的 key的数量                                   |
| flushdb       | 清空当前库                                                   |
| flushall      | 通杀全部库                                                   |

### 字符串**(String)**

| set <key><value>                          | 添加键值对                                                   |
| ----------------------------------------- | ------------------------------------------------------------ |
| get <key>                                 | 查询对应键值                                                 |
| append <key><value>                       | 将给定的<value> 追加到原值的末尾                             |
| strlen <key>                              | 获得值的长度                                                 |
| setnx <key><value>                        | 只有在 key 不存在时 设置 key 的值                            |
| incr <key>                                | 将 key 中储存的数字值增 1<br />只能对数字值操作，如果为空，新增值为 1 |
| decr <key>                                | 将 key 中储存的数字值减 1<br />只能对数字值操作，如果为空，新增值为-1 |
| incrby / decrby <key><步长>               | 将 key 中储存的数字值增减。自定义步长。                      |
| mset <key1><value1><key2><value2> .....   | 同时设置一个或多个 key-value 对                              |
| mget <key1><key2><key3> .....             | 同时获取一个或多个 value                                     |
| msetnx <key1><value1><key2><value2> ..... | 同时设置一个或多个 key-value 对，当且仅当所有给定 key 都不存在。 |
| getrange <key><起始位置><结束位置>        | 获得值的范围，类似 java中的 substring，前包，后包            |
| setrange <key><起始位置><value>           | 用 <value> 覆写<key>所储存的字符串值，从<起始位置>开始(索引从 **0**开始)。 |
| **setex <key><**过期时间**><value>**      | 设置键值的同时，设置过期时间，单位秒。                       |
| getset <key><value>                       | 以新换旧，设置了新值同时获得旧值。                           |

### 列表**(List)**

| lpush/rpush <key><value1><value2><value3> .... | 从左边/右边插入一个或多个值。                   |
| ---------------------------------------------- | ----------------------------------------------- |
| lpop/rpop <key>                                | 从左边/右边吐出一个值。值在键在，值光键亡。     |
| rpoplpush <key1><key2>从<key1>                 | 列表右边吐出一个值，插到<key2>列表左边。        |
| range <key><start><stop>                       | 按照索引下标获得元素(从左到右                   |
| lrange mylist 0 -1                             | 0 左边第一个，-1 右边第一个，(0-1 表示获取所有) |
| lindex <key><index>                            | 按照索引下标获得元素(从左到右)                  |
| llen <key>                                     | 获得列表长度                                    |
| linsert <key> before <value><newvalue>         | 在<value>的后面插入<newvalue>插入值             |
| lrem <key><n><value>                           | 从左边删除 n 个 value(从左到右)                 |
| lset<key><index><value>                        | 将列表 key下标为 index的值替换成 value          |

### 集合**(Set)**

| sadd <key><value1><value2> ..... | 将一个或多个 member 元素加入到集合 key 中，已经存在的 member 元素将被忽略 |
| -------------------------------- | ------------------------------------------------------------ |
| smembers <key>                   | 取出该集合的所有值。                                         |
| sismember <key><value>           | 判断集合<key>是否为含有该<value>值，有 1，没有 0             |
| scard<key>                       | 返回该集合的元素个数。                                       |
| srem <key><value1><value2> ....  | 删除集合中的某个元素。                                       |
| spop <key>                       | 随机从该集合中吐出一个值。                                   |
| srandmember <key><n>             | 随机从该集合中取出 n 个值。不会从集合中删除 。               |
| smove <source><destination>value | 把集合中一个值从一个集合移动到另一个集合                     |
| sinter <key1><key2>              | 返回两个集合的交集元素。                                     |
| sunion <key1><key2>              | 返回两个集合的并集元素。                                     |
| sdiff<key1><key2>                | 返回两个集合的差集元素(key1中的，不包含 key2中的)            |

### 哈希**(Hash)**

| hset <key><field><value>                        | 给<key>集合中的 <field>键赋值<value>                         |
| ----------------------------------------------- | ------------------------------------------------------------ |
| hget <key1><field>                              | 从<key1>集合<field>取出 value                                |
| hmset <key1><field1><value1><field2><value2>... | 批量设置 hash 的值                                           |
| hexists<key1><field>                            | 查看哈希表 key 中，给定域 field 是否存在。                   |
| hkeys <key>                                     | 列出该 hash 集合的所有 field                                 |
| hvals <key>                                     | 列出该 hash 集合的所有 value                                 |
| hincrby <key><field><increment>                 | 为哈希表 key 中的域 field 的值加上增量 1 -1                  |
| hsetnx <key><field><value>                      | 将哈希表 key 中的域 field 的值设置为 value ，当且仅当域 field 不存在 . |

### 有序集合 **Zset(sorted set)**

| zadd <key><score1><value1><score2><value2>...                | 将一个或多个 member 元素及其 score 值加入到有序集 key 当中。 |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| **zrange <key><start><stop> [WITHSCORES]**                   | 返回有序集 key 中，下标在<start><stop>之间的元素带 WITHSCORES，可以让分数一起和值返回到结果集。 |
| zrangebyscore key minmax [withscores] [limit offset count]   | 返回有序集 key 中，所有 score 值介于 min 和 max 之间(包括等于 min 或 max )的成员。有序集成员按 score 值递增(从小到大)次序排列。 |
| zrevrangebyscore key maxmin [withscores] [limit offset count] | 同上，改为从大到小排列。                                     |
| zincrby <key><increment><value>                              | 为元素的 score 加上增量                                      |
| zrem <key><value>                                            | 删除该集合下，指定值的元素                                   |
| zcount <key><min><max>                                       | 统计该集合，分数区间内的元素个数                             |
| zrank <key><value>                                           | 返回该值在集合中的排名，从 0 开始。                          |

### 

