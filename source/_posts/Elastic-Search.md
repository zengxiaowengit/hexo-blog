---
title: Elastic Search
date: 2018-01-17 18:02:46
tags:
	- elastic-search
---


# Elastic Search

## ELK简介

	ES是目前最火的开源全文搜索引擎，基于倒排索引，可以支撑大数据量的检索、排序和TOP N搜索。
	使用ELK技术架构来搭建准实时日志搜索系统也是非常流行的处理方式。

<!-- more -->	

## 基础知识

### 文档(Document)

### 索引(type)

## 环境搭建


## 使用示例


### 查询所有
```json
GET /organization/public/_search
{
  "query": {
    "match_all": {}
  }
}
```

### 标准查询
```json
GET /organization/public/_search
{
  "query": {
    "match": {
      "nameStandard": "江西"
    }
  }
}
```

### 精确值匹配
```json
GET /organization/public/_search
{
  "query": {
    "match": {
      "signStatus": 1
    }
  }
}

```

### 精确值匹配,一般不分词.对于分词字段分词。
```json
GET /organization/public/_search
{
  "query": {
    "term": {
      "nameStandard": {
        "value": "王"
      }
    }
  }
}
```

### 多值匹配-分词
```json
GET /organization/public/_search
{
    "query": {
      "multi_match": {
        "query":    "猎头公司",
        "fields":   [ "nameStandard", "bd.nameStandard" ]
    }
  }
}
```

### 多值匹配
```json
GET /organization/public/_search
{
    "query": {
      "multi_match": {
        "query":    6,
        "fields":   [ "qaStatus", "signStatus" ]
    }
  }
}
```

### bool查询 
```json
GET /organization/public/_search
{
  "query": {
    "bool": {
      "must": [
        {
          "match": {
            "signStatus": 6
          }
        }
      ],
      "must": [
        {
          "match": {
            "nameStandard": "猎头公司"
          }
        }
      ]
    }
  }
}
```


### 查询加结果排序
```json
GET /organization/public/_search
{
  "query": {
    "match": {
      "signStatus": 1
    }
  },
  "sort": [
    {
      "id": {
        "order": "desc"
      }
    }
  ]
}
```

### 查询排序加聚合

	aggs即聚合信息。聚合信息的种类非常多，如：max, min, avg, sum, top N, group by 等。
	基本的聚合信息可以使用stats。
	基本聚合信息不满足的，可以使用extended_stats，有平方和、标准差、方差等。
	
```json
GET /organization/public/_search
{
  "query": {
    "match": {
      "type": 1
    }
  },
  "sort": [
    {
      "id": {
        "order": "desc"
      }
    }
  ],
  "aggs": {
    "statsCnt": {
      "stats": {
        "field": "signStatus"
      }
    }
  }
}
```
```json
{
  "took": 12,
  "timed_out": false,
  "_shards": {
    "total": 5,
    "successful": 5,
    "failed": 0
  },
  "hits": {
    "total": 340,
    "max_score": null,
    "hits": [{
    	...
    }]
  },
  "aggregations": {
    "statsCnt": {
      "count": 340,
      "min": 1,
      "max": 6,
      "avg": 4.2176470588235295,
      "sum": 1434
    }
  }
}
```
	extend_stats输出结果示例:

```json
"aggregations": {
    "statsCnt": {
      "count": 340,
      "min": 1,
      "max": 6,
      "avg": 4.2176470588235295,
      "sum": 1434,
      "sum_of_squares": 6758,
      "variance": 2.0879238754325264,
      "std_deviation": 1.4449650083765095,
      "std_deviation_bounds": {
        "upper": 7.107577075576549,
        "lower": 1.3277170420705104
      }
    }
  }
```
	

## 配置


## 底层原理
