# Exercise - Solution

## SPARQL Query

{% datadotworld "tutorial/sparqltutorial" %}
~~~~
#Return the total POV pages for all characters in house Stark.
PREFIX GOT: <https://tutorial.linked.data.world/d/sparqltutorial/>

SELECT ?FName ?totalPagesPOV

WHERE {
    ?person GOT:col-got-fname ?FName .
    ?person2 GOT:col-got2-name ?FName .
    ?person GOT:col-got-house "Stark" .
    ?person2 GOT:col-got2-totalpagespov ?totalPagesPOV .
}
~~~~
{% enddatadotworld %}

##Congratulations!

You have completed the primer section of the SPARQL tutorial! You are now ready to go run some SPARQL queries on your own data! [Create a dataset](https://data.world/create-a-dataset) with some of your own data or find some existing data on [data.world](https://data.world) and get to SPARQLing!

If you want to help us improve this tutorial, consider taking a brief 2-minute [survey](https://docs.google.com/forms/d/e/1FAIpQLSdF0B8P0wM-Xpm2UCOaKd4xVbnnuyTIu8y2LvuzNYOeQNDJqQ/viewform?usp=sf_link).

Keep an eye out, we will be improving this tutorial over the coming month with new topics and in-depth sections.
