# MongoDB高级操作

[TOC]

## 1 排序

```sql
db.集合.find().sort({需要排序的字段:[1/-1]}) //1升序 -1降序
```

### 准备数据

```sql
use test2;
db.c1.insert({_id:1,name:"a",sex:1,age:1})
db.c1.insert({_id:2,name:"a",sex:1,age:2})
db.c1.insert({_id:3,name:"b",sex:0,age:3})
db.c1.insert({_id:4,name:"c",sex:0,age:4})
db.c1.insert({_id:5,name:"d",sex:0,age:5})

db.c1.find()
```

![image-20201106165012718](img/image-20201106165012718.png)

### 练习：将数据按年龄降序排序

```sql
db.c1.find().sort({age:-1})
```

![image-20201106165420740](img/image-20201106165420740.png)

## 2 分页

```sql
db.集合.find().limit(返回的条数).skip(跳过的条数)
```

### 练习：每页2条，查第二页

```sql
db.c1.find().sort({age:-1}).skip(2).limit(2)
```

![image-20201106165704770](img/image-20201106165704770.png)

```
skip = (起始页-1)*每页条数
limit = 每页条数
```

## 3 统计总条数

```sql
db.c1.find().count([0/1/false/true]) //false、0、不写都表示统计全部数据;true、非0数表示统计限制后的数据
```

**获取限制后的数据**

```sql
db.c1.find().skip(2).count(true)
```

## 4 聚合查询

db.collection.aggregate()是基于数据处理的聚合管道，每个文档通过一个由多个阶段（stage）组成的管道，可以对每个阶段的管道进行分组、过滤等功能，然后经过一系列的处理，输出相应的结果。

大概流程如下：

![](img/image-20201106165704810.png)

```sql
db.集合名称.aggregate([
    {
    	管道:{
    		_id:需要参照的列,
    		查询结果:{表达式:需要处理的列}
    	}
    }
])
```

### 常用管道：

| 管道 | 说明 |
| ---- | ---- |
|$group | 将集合中的文档分组，用于统计结果|
|$match | 过滤数据，只输出符合条件的文档 |
|$sort |  聚合数据进一步排序|
|$skip | 跳过指定文档数|
|$limit | 限制集合数据返回文档数|

### 常用表达式：

| 表达式 | 说明 |
| ------ | ---- |
|$sum | 总和  *$sum:1同count表示统计* |
|$avg | 平均值 |
|$min | 最小值|
|$max | 最大值|

### 准备数据

```sql
use test3;
db.c1.insert({_id:1,name:"a",sex:1,age:1});
db.c1.insert({_id:2,name:"a",sex:1,age:2});
db.c1.insert({_id:3,name:"b",sex:2,age:3});
db.c1.insert({_id:4,name:"c",sex:2,age:4});
db.c1.insert({_id:5,name:"d",sex:2,age:5});
```

### 练习1：统计男生、女生的总年龄

```sql
db.c1.aggregate([
    {
        $group: {
            _id: "$sex",
            总数: {
                $sum: "$age"
            }
        }
    }
])
```

![image-20201107102909740](img/image-20201107102909740.png)

此时_id中的值对应c1中sex列的值。

### 练习2：统计男女生的总人数

```sql
db.c1.aggregate([
    {
        $group: {
            _id: "$sex",
            总数: {
                $sum: 1
            }
        }
    }
])
```

![image-20201107102802038](img/image-20201107102802038.png)

### 练习3：求学生总数和平均年龄

```sql
db.c1.aggregate([
    {
        $group: {
            _id: null,
            学生总数: {
                $sum: 1
            },
            平均年龄: {
                $avg: "$age"
            }
        }
    }
])
```

![image-20201107103600673](img/image-20201107103600673.png)

### 练习4：查询男生、女生人数，按人数升序

```sql
db.c1.aggregate([
    {
        $group: {
            _id: "$sex",
            人数: {
                $sum: 1
            }
        }
    },
    {
        $sort: {
            人数: -1
        }
    }
])
```

![image-20201107104335167](img/image-20201107104335167.png)

## 5 优化索引

```sql
db.集合.createIndex({索引的列:[1/-1]})// 1表示升序,-1表示降序
```

