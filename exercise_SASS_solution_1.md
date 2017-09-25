# Exercise - Solution 1

In this solution, we use the MIN and MAX aggregate functions to find the min and max values.

Part A solution:

{% datadotworld "tutorial/sparqltutorial" %}
~~~~
# Find the lowest age in the dataset.

PREFIX GOT: <https://tutorial.linked.data.world/d/sparqltutorial/>

SELECT (MIN(?age) as ?minAge)

WHERE {
  ?person GOT:col-got-age ?age .
}
~~~~
{% enddatadotworld %}

Part B solution:

{% datadotworld "tutorial/sparqltutorial" %}
~~~~
# Find the highest age in the dataset.

PREFIX GOT: <https://tutorial.linked.data.world/d/sparqltutorial/>

SELECT (MAX(?age) as ?maxAge)

WHERE {
  ?person GOT:col-got-age ?age .
}
~~~~
{% enddatadotworld %}

## Next Section: [Grouping Your Data](./Grouping_Your_Data.md)
