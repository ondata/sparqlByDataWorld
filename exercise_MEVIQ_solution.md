# Exercise - Solution

{% datadotworld "tutorial/sparqltutorial" %}
~~~~
#Display all the people associated with House Stark.

PREFIX GOT: <https://tutorial.linked.data.world/d/sparqltutorial/>

SELECT ?FName

WHERE {
  ?person GOT:col-got-house "Stark" .
  ?person GOT:col-got-fname ?FName .
}
~~~~
{% enddatadotworld %}

If your query didn't return Jon's name, you most likely searched for "Stark" using the `GOT:col-got-lname` property name instead of the `GOT:col-got-house` property name.

## Next Section: [Sorting and Summary Statistics](./Sorting_and_Summary_Statistics.md)
