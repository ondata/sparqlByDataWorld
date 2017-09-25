# Exercise - Solution

## SPARQL Query:

{% raw  %}
~~~~
PREFIX GOT: <https://tutorial.linked.data.world/d/sparqltutorial/>

SELECT ?name ?birthMonth

WHERE {
    ?person GOT:col-got-fname ?FName ;
            GOT:col-got-lname ?LName ;
            GOT:col-got-birthdate ?birthDate .
    BIND (MONTH(?birthDate) AS ?birthMonth)
    BIND (CONCAT(?FName, " ", ?LName) AS ?name)
    FILTER(?birthMonth = 4)
}
~~~~
{% endraw  %}

##Next Section: [Linking Datasets Together](./Linking_Datasets_Together.md)
