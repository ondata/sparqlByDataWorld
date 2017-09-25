# Exercise - Solution

## SPARQL Query

{% raw  %}
~~~~
#The average age of each house within our dataset.

PREFIX GOT: <https://tutorial.linked.data.world/d/sparqltutorial/>

SELECT ?house (AVG(?age) AS ?avgAge)

WHERE {
	?person GOT:col-got-house ?house ;
        	GOT:col-got-age ?age .
}
GROUP BY ?house
~~~~
{% endraw  %}

## Next Section: [Filtering Your Data](./Filtering_Your_Data.md)
