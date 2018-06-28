# data_format

### query_data

```
#[Concept, Entity, Relation, Attribute, Value]
{
    "query":"中国的首都在哪里",
    "query_tagger":"[中国@Entity]的[首都@Relation]在哪里",
    "ner":[
            {"startidx":0, "length":2, "type":"Entity", "mention":"中国", "uri":"中国（四大文明古国之一）"},
            {"startidx":3, "length":2, "type":"Relation", "mention":"首都", "uri":"首都"},
            ],
    "ner_count":{
                    "concept":0,
                    "entity":1,
                    "relation":1,
                    "attribute":0,
                    "value":0
                },
    "ner_seq":"ER",
    "word_tagger":{
                    Word("中国","Entity","中国uri"),
                    Word("的","other","的"),
                    Word("首都","Relation","首都uri"),
                    Word("在哪里","other","在哪里"),
                  },
    "template":"entity + Other_or_None + relation",
    "func":"entity_SP_",
    #"sort":{...},
    "SPARQL":"...",
    "reply":"北京",
}
```

### template

```
rules = [{temp1},{temp2},...]
temp:
{
    "condition_num":2,
    "template":entity+Star(W(pos='other'),greedy=False)+relation,
    "template_str":'''entity+Star(W(pos='other'),greedy=False)+relation''',
    "slot":(subject, predicate),
    "func":self.question_set.entity_SP_,
}
```

