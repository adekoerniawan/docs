# elasticsearch
---
## _index
索引就是文档集合
## _type
类型是索引的一个分区

### match_all
```
GET /bank/_search
{
  "query": { "match_all": {} },
  "_source":["name", "age"],//返回字段设置
  "sort": [{ "age": "asc" }],
  "from":10,
  "size":10
}
```
### match
{"name":"hello world"}查询name字段包含“hello”或“world”的
```
GET /mytest/user/_search
{
  "query": {
    "match": {"name_text":"Tom cat"}
  },
  "_source": ["name_keyword", "age"],
  "size":3
}
```
### match_phrase
{"name":"hello world"}查询name字段包含“hello world”的
```
GET /mytest/user/_search
{
  "query": {
    "match_phrase": {"name_text":"cat"}
  }
}
```
### bool
将小的查询组成大的查询
bool must 且
bool should 或
bool must_not 非
```
GET /mytest/user/_search
{
  "query": {
    "bool": {
      "must": [
        { "match": { "name_text": "tom" } },
        { "match": { "name_text": "cat" } }
      ]
    }
  }
}
```

keyword精确匹配查找
text模糊匹配查找

