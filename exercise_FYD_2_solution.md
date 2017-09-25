#Exercise 2 - Solution

##SPARQL Query

{% raw  %}
~~~~
#Return the first name and last name of all the characters in our dataset born after year 265 *and* before year 285.

PREFIX GOT: <https://tutorial.linked.data.world/d/sparqltutorial/>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>

SELECT ?FName ?LName

WHERE {
    ?person GOT:col-got-fname ?FName .
    ?person GOT:col-got-lname ?LName .
    ?person GOT:col-got-birthdate ?BirthDate .
    FILTER (?BirthDate > "0265-01-01"^^xsd:date && ?BirthDate < "0285-12-31"^^xsd:date)
}
~~~~
{% endraw  %}

Or we can use a slightly different syntax (the results are the same):

{% raw  %}
~~~~
#Return the first name and last name of all the characters in our dataset born after year 265 *and* before year 285.

PREFIX GOT: <https://tutorial.linked.data.world/d/sparqltutorial/>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>

SELECT ?FName ?LName

WHERE {
    ?person GOT:col-got-fname ?FName .
    ?person GOT:col-got-lname ?LName .
    ?person GOT:col-got-birthdate ?BirthDate .
    FILTER (?BirthDate > "0265-01-01"^^xsd:date)
    FILTER (?BirthDate < "0285-12-31"^^xsd:date)
}
~~~~
{% endraw  %}

##Next Section: [Introduction to Data Munging](./Introduction_to_Data_Munging.md)
