# Exercise 1 - Solution

## SPARQL Query

{% datadotworld "tutorial/sparqltutorial" %}
~~~~
#Return the first and last name of all characters in our dataset 17 years of age or younger.

PREFIX GOT: <https://tutorial.linked.data.world/d/sparqltutorial/>

SELECT ?FName ?LName ?Age

WHERE {
    ?person GOT:col-got-fname ?FName .
    ?person GOT:col-got-lname ?LName .
    ?person GOT:col-got-age ?Age .
    FILTER (?Age <= 17)
}
ORDER BY ?Age
~~~~
{% enddatadotworld %}

##Next Exercise
When you're ready, try the next [exercise](./exercise_FYD_2.md).
