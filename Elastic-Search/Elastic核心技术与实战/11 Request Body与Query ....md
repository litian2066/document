# Request Body与Query ...

## Request Body Search

![image-20220510143852119](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220510143852119.png)

## 分页

![image-20220510143935963](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220510143935963.png)

## 排序

![image-20220510144003505](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220510144003505.png)

## _source filtering

![image-20220510144047377](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220510144047377.png)

## 脚本字段

![image-20220510144344890](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220510144344890.png)

![image-20220510144437360](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220510144437360.png)

## 使用查询表达式 - Match

> 以下例子默认是OR的关系，即查询comment字段包含Last 或者 Christmas的信息，如果需要查询两个词汇都有，那么需要添加Operator信息

````shell
POST movies/_search
{
  "query": {
    "match": {
      "title": "Last Christmas"
    }
  }
}
````

![image-20220510145112702](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220510145112702.png)

````shell
POST movies/_search
{
  "query": {
    "match": {
      "title": {
        "query": "Last Christmas",
        "operator": "and"
      }
    }
  }
}
````

![image-20220510145243162](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220510145243162.png)

## 短语搜索 - Match Phrase

![image-20220510144813556](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220510144813556.png)

```shell
POST movies/_search
{
  "query": {
    "match_phrase": {
      "title": {
        "query": "one love"
      }
    }
  }
}
```

![](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220510145535843.png)

通过slot可以允许单词之间插入几个单词

![image-20220510145603830](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220510145603830.png)