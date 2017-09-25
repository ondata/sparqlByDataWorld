# Grouping Your Data
We've already learned how to find maximums, sum values, and perform other such manipulations to a dataset. Now it's time to combine that with a SPARQL function called GROUP BY. GROUP BY aggregates data in your dataset, making it easy to run functions like MAX on a part or parts of your data.

##KEYWORDS and concepts you will learn

* GROUP BY - partitioning the data into groups for analysis
* How to combine aggregation functions such as MAX and MIN with GROUP BY to tell new stories about the data

###Aggregation using GROUP BY

SPARQL's GROUP BY function lets us link SPARQL's aggregation functions with other data in our datasets. This is one of SPARQL's most powerful features, and let's us make new discoveries and tell new stories with our data.

Recall in exercise 3 we learned how to find the maximum age of any character in the data by using

```
SELECT (MAX(?age) as ?maxAge)
```

which bound maxAge as the maximum age of any character in the dataset.

Now what if we want to find the maximum age of any character within each house? We can do this by using SPARQL's GROUP BY function:

{% datadotworld "tutorial/sparqltutorial" %}
~~~~
PREFIX GOT: <https://tutorial.linked.data.world/d/sparqltutorial/>

SELECT ?house (MAX(?age) as ?maxAge)

WHERE {
	?person GOT:col-got-house ?house ;
        	GOT:col-got-age ?age .
}
GROUP BY ?house
~~~~
{% enddatadotworld %}

---
### What's with the semicolon?
You may have noticed that this query looks a little different then the previous ones we wrote. If you're using the same resource (?person) with different properties (GOT:col-got-house and GOT:col-got-age) you can skip rewriting the resource. Simply end each new statement with a semicolon, and end the last one with a period. What we wrote above is interpreted exactly the same as:

```
?person GOT:col-got-house ?house .
?person GOT:col-got-age ?age .
```
---

We could use any of [SPARQL's Aggregate Functions](./list_of_sparql_aggregate_functions.md) in place of MAX within the above query. Try a few and see what happens. Remember that it might be worth changing the variable ?maxAge to something more relevant to what your query outputs.

###Why is this useful?

Imagine you have a dataset comprising answers to a survey on alcohol habits. This dataset includes

* Zip Code
* Age
* Drinks per week consumed

Using GROUP BY for "Zip Code" with SPARQL's aggregation function AVG on drinks per week would let you find the average number of drinks consumed for all zip codes in the study.

###Exercise

Now you are ready to try [the exercise](./exercise_GYD.md).
