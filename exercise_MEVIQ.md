# Exercise - Matching Exact Values

## Your task

Write a SPARQL query that displays all the people associated with House Stark.

Use the workspace below to draft your SPARQL query using a string literal to find the exact value "Stark" in the data.

{% datadotworld "tutorial/sparqltutorial" %}
~~~~
PREFIX GOT: <https://tutorial.linked.data.world/d/sparqltutorial/>
~~~~
{% enddatadotworld %}

## Having trouble?

Just like Exercise 1, this query's WHERE section should follow the same format as an RDF data statement:
```
{ resource propertyName propertyValue }.
```
The resource will be a variable of your choosing to store data found by the query. For the propertyName, be sure not to mix up the House and LName properties; not all people associated with House Stark have Stark as their last name. The propertyValue will be your string literal.

## Ready for the solution?
Head over to [the solution](./exercise_MEVIQ_solution.md) to see our implementation of the solution.
