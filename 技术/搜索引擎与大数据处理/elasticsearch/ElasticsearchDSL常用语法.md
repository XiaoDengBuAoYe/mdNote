## DSL 介绍

### 索引库

#### 创建

```yaml

PUT /索引库名称 
{
  "mappings": {
    "properties": {
      "字段一": {
        "type": "text", # 字段类型
        "analyzer": "ik_smart" #分词器
      },
      "字段二": {
        "type": "integer",
        "index": false # 索引  是否参与搜索
      },
      "字段二": {
        "type": "object",
        "properties": {
              "字段一": {
                "type": "text"
              },
      	}
      },
    }
}

```

#### 修改

```
索引库和mapping一旦创建就不能修改，但是可以添加新的字段，新添加的字段名字不能和之前一样
PUT /索引库名/_mapping
{
	"properties":{
		"新字段名":{
			"type":"data"
		}
	}
}
```



### 基础CRUD

#### 新增

```java
POST /索引库名/_doc/文档id
{
	"字段一": "值一",
	"字段二": "值二",
	"字段三": {	
		"字段三-一":"值",
		...
	},
	...
}
```

#### 删除

```
DELETE /索引库名/_doc/文档id
```

#### 查看

```
GET /索引库名/_doc/文档id
```

#### 修改

##### 方式1

全量修改，删除原文档，生成新文档

```json
PUT /索引库名/_doc/文档id
{
	"字段一": "值一",
	"字段二": "值二",
	"字段三": {	
		"字段三-一":"值",
		...
	},
	...
}
```



##### 方式2

特定字段修改

```java
POST /索引库名/_update/文档id
{
	"字段名": "新值",
}
```





###  DSL Query 简单查询

#### 模板

```json
Get /索引库名/_search
{
 "query": {
	"查询类型": {
        "查询条件": "值"
    }
  }
}
```



#### 查询所有

```json
Get /索引库名/_search
{
 "query": {
	"match_all": {}
  }
}
```



#### 全文检索查询

> 会对输入的内容分词，常用于搜索框

```json
//推荐第一个，建议吧多个字段拷到一个字段
Get /索引库名/_search
{
 "query": {
	"match":{//match模式   单字段,但是可以查询之前连锁的字段
        "字段": "内容"
    }
  }
}



Get /索引库名/_search
{
 "query": {
	"multi_match":{//multi_match模式 与match模式类似 可以多字段查询 
        "query": "内容",
        "fields": ["a字段","b字段","c字段"]
    }
  }
}
```



#### 精确查询

> 一般日期，数值，身份证 等

```json
// term查询 不会分词
Get /索引库名/_search
{
 "query": {
	"term":{
        "city": {
            "value": "上海"
        }
    }
  }
}

// range查询 范围查询
Get /索引库名/_search
{
 "query": {
	"range":{
        "price": {
            "gte": 100,
            "lte": 300,
        }
    }
  }
}
```

| 符号标识 | 代表含义   |
| -------- | ---------- |
| gte      | 大于或等于 |
| gt       | 大于       |
| lte      | 小于或等于 |
| lt       | 小于       |



#### 地理查询

```json
//查询值是否在某矩形范围内
Get /索引库名/_search
{
 "geo_bounding_box": {
	"字段名":{
        "top_left": {
            "lat": 31.1,
            "lon": 121.5
        },
         "bottom_right": {
            "lat": 30.9,
            "lon": 121.7
        }
    }
  }
}

//查询到指定中心点小于某个距离值的所有文档
Get /索引库名/_search
{
 "geo_distancex": {
     "distance": "15km", //距离
     "字段名": "121.5,XXX.X"//中心点
  }
}
```



### DSL Query 复杂查询

#### 修改算分规则

> query score 查询的相关分数
>
> 使用function score query 来修改相关性规则，从而改变查询排序

```json
Get /索引库名/_search
{
 "function_ score": {
     "query": "{}", //简单查询 ，查询相关数据
     "functions": [
         {
             "filter": {
                 "term":{
                     //精确查询(过滤条件),查询到的数据文档重新使用下面的函数重新算分
                 }
             },
             "weight":  10//这里值为算分函数 ,用来进行算分 
         },
         "boost_mode": "multiply" //加权模式 定义function score和query score的运算模式
     ]
  }
}
```

##### 常见的算分函数

|      算分函数      |             作用             |
| :----------------: | :--------------------------: |
|       weight       |  给一个常量值，作为函数结果  |
| field_value_factor | 文档中某个字段值作为函数结果 |
|    random_score    |      随机值作为函数结果      |
|    script_score    |        自定义计算公式        |

##### boost_mode 加权模式

|   模式   |         作用          |
| :------: | :-------------------: |
| multiply |    两者相加，默认     |
| replace  | function分替换query分 |
|   其他   |    sum;max;min;avg    |



#### 复合查询(子查询)



| 布尔查询 | 作用                        |
| -------- | --------------------------- |
| must     | 必须；类似 与               |
| should   | 选择 ； 类似 或             |
| must_not | 必须不; 不参与算分  类似 非 |
| filter   | 必须 不参与算分             |

```json
Get /索引库名/_search
{
 "bool": {
     "must": [
         {
             "term": {
                 xx : xx
             }
         }
     ],
     "should":[
         {
             "term" :{
                 xx : aa
             },
             "term" :{
                 xx : bb
             }
         }
     ],
     "must_not": [
         {
             "range" : {
                 
             }
         }
     ],
     "filter":[
         {
             "range" : {
                 
             }
         }
     ]
  }
}
```



#### 排序

> es支持对搜索结果进行排序，默认是根据相关度算分排序，可以排序的字段类型keyword(字符串)，数值，地理坐标，日期等
>
> 写了这个排序就不再算分

```json
Get /索引库名/_search
{
 "query": {

  },
  "sort":[
      {
          "字段名" : "desc"  //排序字段和排序方式
      },
      {
          "-geo_distance" :{
              "字段名" : "纬度，经度",//中心点，可以写字符串也可以写对象{"lat":xx.xx,"lon:xx.xx"}
              "order": "asc",//升降序
              "unit" : "km"// 显示单位
          }
      }
  ]
}
```



#### 分页

> 跟 mysql分页底层不同 ，使用的是逻辑分页，查出来再拆出来，
>
> 比如要查询第十页的十条数据要查询10*10的数据然后截取第90到100
>
> 集群的话会每个集群都查出来100条，然后结果汇总再排序截取
>
> 从而造成 深度分页问题  ,只能从根源上杜绝，比如最大搜索页数(京东最大查询100页)
>
> 默认结果集最大10000条数据

```json
Get /索引库名/_search
{
 "query": {
  },
  "from":  10 ,  //分页 开始的位置 默认0
  "size" : 10, //期望获取的文档总数
}
```

##### 解决深度分页

search after : 分页时排序，原理是从上一次的排序开始，查询下一页数据。（没有查询上限，只能向后翻页，不能随机翻页）

scroll： 保存快照到内存。官方不推荐(占内存,数据不同步)

#### 搜索结果处理（高亮）

```json
Get /索引库名/_search
{
 "query": {
        "match": :{
         "字段名": "内容"
         }
  },
"highlight" :{
    "fields":{
        "字段名":{//需要处理的高亮字段
            "require_field_match": "false",//匹配的字段高亮，true是查询到的字段高亮
            "pre_tags":"<em>",//高亮前置标签
            "post_tags":"</em>"//高亮后置标签
        }
    }
}
}
```

