# Exercise - Solution 2

In this solution, we use ORDER BY and LIMIT to find the min and max values.

Part A solution:

{% raw  %}
~~~~
# Find the lowest age in the dataset.

PREFIX GOT: <https://tutorial.linked.data.world/d/sparqltutorial/>

SELECT ?age

WHERE {
  ?person GOT:col-got-age ?age .
}
ORDER BY ?age
LIMIT 1
~~~~
{% endraw  %}

Part B solution:

{% raw  %}
~~~~
# Find the highest age in the dataset.

PREFIX GOT: <https://tutorial.linked.data.world/d/sparqltutorial/>

SELECT ?age

WHERE {
  ?person GOT:col-got-age ?age .
}
ORDER BY DESC(?age)
LIMIT 1
~~~~
{% endraw  %}

## Next Section: [Grouping Your Data](./Grouping_Your_Data.md)
