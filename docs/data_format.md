# data_format

### query_data

```
#[Concept, Entity, Relation, Attribute, Value]
{
    "query":"中国的首都在哪里",
    "query_tagger":"[中国@Entity]的[首都@Relation]在哪里",
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
    "template":"entity+Star(W(pos='other'),greedy=False)+relation",
    "func":"entity_SP_",
    "SPARQL":"",
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
    "func":self.question_set.entity_SP_,
}
```

