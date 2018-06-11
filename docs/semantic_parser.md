# semantic_parser
---
## question type
* **事实类fact**

    * 统计类count
        > * 中国有多少个省？
        ```
        select (count(?x) as ?num) where
        {
	        ?x :type "province".
	        ?x :所属国家 "中国".
        }
        ```
        > * 人口超过1000万的城市有多少个？
        ```
        select (count(?x) as ?num) where
        {
	        ?x :type "city".
	        ?x :人口 ?p.
	        filter(?p > 10e6).
        }
        ```
    
    * 排序类max，min
        > * 人口最多的国家是哪个？
        ```
        select ?x where
        {
	        ?x :type "country".
	        ?x :人口 ?p.
        }
        order by desc (?p) #desc:降序, asc:升序
        LIMIT 1
        ```
        > * 中国哪个省的面积最小？
        ```
        select ?x where
        {
	        ?x :type "province".
	        ?x :所属国家 "中国".
	        ?x :面积 ?a.
        }
        order by asc (?p) #desc:降序, asc:升序
        LIMIT 1
        ```
    
    * 判断类yes/no
        > * 苏州是不是江苏的省会啊？
        ```
        ask
        {
            "江苏" :省会 "苏州".
        }
        ```
        > * 苏州的人口超过1000万了吗？
        ```
        ask
        {
            "苏州" :人口 ?p.
            filter(?p > 10e6).
        }
        ```
        > * 印度的人口超过中国了吗？
        ```
        ask
        {
            "印度" : ?p1.
            "中国" : ?p2.
            filter(?p1 > ?p2)
        }
        ```
    
    * 选择类choice
        > * 江苏的省会是苏州还是南京啊？
        ```
        /* fix */
        select distinct ?x where
        {
            "江苏" :省会 ?x
        }
        ```
        > * 杭州是江苏的省会还是浙江的省会？
        ```
        /* fix */
        select distinct ?x where
        {
            ?x :省会 "杭州"
        }
        ```
        > * 苏州是江苏的省会还是浙江的省会？
        ```
        todo
        ```
        > * 南京、苏州和杭州哪个是省会城市？
        ```
        todo
        ```
    
    * 比较类compare
        > * 北京和上海哪个人口多？
        ```
        select ?x where
        {
	        {?a :S_name :"北京"}
	        union
	        {?a :S_name :"上海"}
	        ?a :人口 ?p.
	        ?a :S_name ?x.
        }
        order by desc (?p) #asc
        LIMIT 1
        ```
        > * 中国的面积大还是美国的面积大？
        ```
        select ?x where
        {
	        {?country :S_name :"中国"}
	        union
	        {?country :S_name :"美国"}
	        ?country :面积 ?a.
	        ?country :S_name ?x.
        }
        order by desc (?a) #asc
        LIMIT 1
        ```
    
    * 描述类description
        > * 你知道虎丘吗？
        ```
        select ?x where
        {
            "虎丘" :description ?x.
        }
        ```
    
    * 填槽类slot
        > * 中国的首都是哪里？< S, P, ? >
        ```
        select distinct ?x
        {
            "中国" :首都 ?x.
        }
        ```
        > * 北京是哪个国家的首都？< ?, P, O>
    ```
    select distinct ?x
        {
            ?x :首都 "北京".
        }
        ```
        > * 北京和中国是什么关系？< S, ?, O>
        ```
        select distinct ?x
        {
            "中国" ?x "北京".
        }
        ```
        > * 中国的首都的人口是多少？< S, P1, x> < x P2, ?>
        ```
        select distinct ?x
        {
            "中国" :首都 ?c.
            ?c :人口 ?x.
        }
        ```
    
* **观点类**

    * how
        > * 你觉得苏州这个城市怎么样啊？
        ```
        unknown
        ```
    
    * why
        > * 为什么苏州的外来人口这么多？
        ```
        unknown
        ```

## question parser
----
### 1. 成分句法分析（stanford）

### 2. 依存句法分析（ltp）

### 3. 语义角色标注（ltp）

### 4. 语义解析（smantic parsing）