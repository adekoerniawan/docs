# semantic_parser
---
## question type
* **事实类fact**

    * 统计类count
        > * 中国有多少个省？
        ```sparql
        SELECT (count(?x) as ?num) WHERE
        {
	        ?x :type "province".
	        ?x :所属国家 "中国".
        }
        ```
        > * 人口超过1000万的城市有多少个？
        ```sparql
        SELECT (count(?x) as ?num) WHERE
        {
	        ?x :type "city".
	        ?x :人口 ?p.
	        FILTER(?p > 10e6).
        }
        ```
    
    * 排序类max，min
        > * 人口最多的国家是哪个？
        ```sparql
        SELECT ?x WHERE
        {
	        ?x :type "country".
	        ?x :人口 ?p.
        }
        ORDER BY DESC (?p) #desc:降序, asc:升序
        LIMIT 1
        ```
        > * 中国哪个省的面积最小？
        ```sparql
        SELECT ?x WHERE
        {
	        ?x :type "province".
	        ?x :所属国家 "中国".
	        ?x :面积 ?a.
        }
        ORDER BY ASC (?p) #desc:降序, asc:升序
        LIMIT 1
        ```
    
    * 判断类yes/no
        > * 苏州是不是江苏的省会啊？
        ```sparql
        ASK
        {
            "江苏" :省会 "苏州".
        }
        ```
        > * 苏州的人口超过1000万了吗？
        ```sparql
        ASK
        {
            "苏州" :人口 ?p.
            FILTER(?p > 10e6).
        }
        ```
        > * 印度的人口超过中国了吗？
        ```sparql
        ASK
        {
            "印度" : ?p1.
            "中国" : ?p2.
            FILTER(?p1 > ?p2)
        }
        ```
    
    * 选择类choice
        > * 江苏的省会是苏州还是南京啊？
        ```sparql
        # fix
        SELECT DISTINCT ?x WHERE
        {
            "江苏" :省会 ?x
        }
        ```
        > * 杭州是江苏的省会还是浙江的省会？
        ```sparql
        # fix
        SELECT DISTINCT ?x WHERE
        {
            ?x :省会 "杭州"
        }
        ```
        > * 苏州是江苏的省会还是浙江的省会？
        ```sparql
        todo
        ```
        > * 南京、苏州和杭州哪个是省会城市？
        ```sparql
        todo
        ```
    
    * 比较类compare
        > * 北京和上海哪个人口多？
        ```sparql
        SELECT ?x WHERE
        {
	        {?a :S_name :"北京"}
	        union
	        {?a :S_name :"上海"}
	        ?a :人口 ?p.
	        ?a :S_name ?x.
        }
        ORDER BY DESC (?p)
        LIMIT 1
        ```
        > * 中国的面积大还是美国的面积大？
        ```sparql
        SELECT ?x WHERE
        {
	        {?country :S_name :"中国"}
	        UNOIN
	        {?country :S_name :"美国"}
	        ?country :面积 ?a.
	        ?country :S_name ?x.
        }
        ORDER BY DESC (?a)
        LIMIT 1
        ```
    
    * 描述类description
        > * 你知道虎丘吗？
        ```sparql
        SELECT ?x WHERE
        {
            "虎丘" :description ?x.
        }
        ```
    
    * 填槽类slot
        > * 中国的首都是哪里？< S, P, ? >
        ```sparql
        SELECT DISTINCT ?x WHERE
        {
            "中国" :首都 ?x.
        }
        ```
        > * 北京是哪个国家的首都？< ?, P, O>
        ```sparql
        SELECT DISTINCT ?x WHERE
        {
            ?x :首都 "北京".
        }
        ```
        > * 北京和中国是什么关系？< S, ?, O>
        ```sparql
        SELECT DISTINCT ?x WHERE
        {
            "中国" ?x "北京".
        }
        ```
        > * 中国的首都的人口是多少？< S, P1, x> < x P2, ?>
        ```sparql
        SECLECT DISTINCT ?x WHERE
        {
            "中国" :首都 ?c.
            ?c :人口 ?x.
        }
        ```
    
* **观点类**

    * how
        > * 你觉得苏州这个城市怎么样啊？
        ```sparql
        unknown
        ```
    
    * why
        > * 为什么苏州的外来人口这么多？
        ```sparql
        unknown
        ```

## question parser
----
### 1. 成分句法分析（stanford）

### 2. 依存句法分析（ltp）

### 3. 语义角色标注（ltp）

### 4. 语义解析（smantic parsing）