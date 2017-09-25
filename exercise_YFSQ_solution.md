# Exercise - Solution

Your query may not look exactly like ours. You may have used different variable names or ordered the statements of the WHERE section differently. These small differences are okay; it's the results that matter.

{% raw  %}
~~~~
#Display the first and last names of all characters in the data.

PREFIX GOT: <https://tutorial.linked.data.world/d/sparqltutorial/>

SELECT ?FName ?LName

WHERE {
  ?person GOT:col-got-fname ?FName .
  ?person GOT:col-got-lname ?LName .
}
~~~~
{% endraw  %}

## Next Section: [Matching Exact Values In Queries](./Matching_Exact_Values_In_Queries.md)
