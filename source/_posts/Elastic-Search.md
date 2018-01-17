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

### 精确值匹配,不分词.对于分词字段分词 
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


### 排序
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



## 配置


## 底层原理
