# Linking Datasets Together

##In this section you will learn:

* How to access multiple datasets within one query

### Bringing your data together

Now let's actually link up some data! You might have noticed that we have two datasets in the tutorial page on data.world. [GOT.csv](https://data.world/tutorial/sparqltutorial/file/GOT.csv) has names, ages, houses and birthdates for our characters. The [GOT2.csv](https://data.world/tutorial/sparqltutorial/file/GOT2.csv) has listings of the number of pages in each book that are from each character's point of view (POV).

Using the power of SPARQL queries, we can query and manipulate data from both of these datasets within one query. Here's an example:

{% datadotworld "tutorial/sparqltutorial" %}
~~~~
PREFIX GOT: <https://tutorial.linked.data.world/d/sparqltutorial/>

SELECT ?FName ?age ?book1PagesPOV

WHERE {
    ?person GOT:col-got-fname ?FName .
    ?person2 GOT:col-got2-name ?FName .
    ?person GOT:col-got-age ?age .
    ?person2 GOT:col-got2-book1pagespov ?book1PagesPOV .
}
~~~~
{% enddatadotworld %}

Go ahead and run this. Note that the results contain the age and number of pages from book1 that are from each character's POV.

This works because the first name from *GOT.csv* matches the name in *GOT2.csv*, and so the data gets linked together. Notice that we use `?person` and `?person2` to get the entries from both of the datasets. The `?person` resource corresponds to the first dataset, and the `?person2` resource corresponds to the second.

Now we can start doing some interesting stuff. Here's an example where we take characters who have an age entry and find out what percentage of their total POV pages are in book 1:

{% datadotworld "tutorial/sparqltutorial" %}
~~~~
PREFIX GOT: <https://tutorial.linked.data.world/d/sparqltutorial/>

SELECT ?FName ?age (?book1PagesPOV / ?totalPagesPOV * 100 AS ?book1Percent)

WHERE {
    ?person GOT:col-got-fname ?FName .
    ?person2 GOT:col-got2-name ?FName .
    ?person GOT:col-got-age ?age .
    ?person2 GOT:col-got2-book1pagespov ?book1PagesPOV .
    ?person2 GOT:col-got2-totalpagespov ?totalPagesPOV .
}
ORDER BY DESC(?age)
~~~~
{% enddatadotworld %}

### Why is this useful?

Imagine you've got some data about political leanings, that's grouped by zip code. If you could find US census data that's also grouped by zip code, you can join *link* these two datasets together and see if you can find interesting correlations between demographics and political leanings, by zip code.

### Exercise

This is just the beginning of what can be done with the power of linked data. Head on over to [the exercise](./exercise_LDT.md) to try for yourself.
