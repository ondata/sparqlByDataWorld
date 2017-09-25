# Filtering Your Data
The last section covered how to find a specific piece of info about a dataset, like the max age of any character in our Game of Thrones data. Now we are going to explore how to filter datasets to return data that are useful to us, using SPARQL's FILTER function.

##KEYWORDS and concepts you will learn:

* FILTER - filter queries to return useful results
* The various filtering functions that SPARQL makes available to you
* How SPARQL handles dates and times

### FILTER

What if we want to return all characters in our dataset above a certain age? We can do this using SPARQL's FILTER function. This is a query that returns the first and last name of all characters in our dataset above 10 years of age:

{% raw  %}
~~~~
PREFIX GOT: <https://tutorial.linked.data.world/d/sparqltutorial/>

SELECT ?FName ?LName ?Age

WHERE {
	?person GOT:col-got-fname ?FName .
    ?person GOT:col-got-lname ?LName .
    ?person GOT:col-got-age ?Age .
	FILTER (?Age > 10)
}
~~~~
{% endraw  %}

The FILTER function allows us to, as expected, filter for the results we want from the query.
In this example we took the variable we are filtering for and applied one of SPARQL's filter functions. In this case it looks like:

```
FILTER (?Age > 10)
```

Note that this filters *for* any characters above 10, the same as filtering *out* any characters with ages less than or equal to 10. For a list of SPARQL's filter functions (such as "<", "=", "<=" and more) see: [List of SPARQL Filter Functions](./list-of-sparql-filter-functions.md)

###Ordering our Filtered Results

Notice that these results are listed by their place within our dataset, instead of ordered by age. We already know how to order our results, so let's make the change we need to order the results so that the highest age comes first.

{% raw  %}
~~~~
PREFIX GOT: <https://tutorial.linked.data.world/d/sparqltutorial/>

SELECT ?FName ?LName ?Age

WHERE {
	?person GOT:col-got-fname ?FName .
    ?person GOT:col-got-lname ?LName .
    ?person GOT:col-got-age ?Age .
	FILTER (?Age > 10)
}
ORDER BY DESC(?Age)
~~~~
{% endraw  %}

Now we have a listing of all characters in our data set older than 10, ordered from oldest to youngest.

###Filtering by Date

Now let's try something slightly different. We want to return the first name and last name of all characters in our dataset born before the year 270.

You may have noticed that within our dataset "GOT" we have a column titled "BirthDate". This column contains the (approximate) birthdates of all of our characthers in a standard formatting (yyyy-mm-dd). data.world automatically reads in these dates, and allows us to filter them in the same way we would an integer (like age). In action, it looks like this:

```
FILTER (?BirthDate < "0280-01-01"^^xsd:date)
```

We put the date in quotes and add "^^xsd:date" after to signify that this value is a date and not an integer. This line will filter for any BirthDate that comes before January 1st, 280.

Here's what the whole query looks like:

{% raw  %}
~~~~
PREFIX GOT: <https://tutorial.linked.data.world/d/sparqltutorial/>
PREFIX xsd:<http://www.w3.org/2001/XMLSchema#>

SELECT ?FName ?LName ?BirthDate

WHERE {
	?person GOT:col-got-fname ?FName .
    ?person GOT:col-got-lname ?LName .
    ?person GOT:col-got-birthdate ?BirthDate .
	FILTER (?BirthDate < "0280-01-01"^^xsd:date)
}
~~~~
{% endraw  %}

Notice that we added the prefix:

```
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
```

Don't worry about this for now, just know we need it if we want to filter or otherwise manipulate dates in our SPARQL queries.

This query returns a table of all of our characters born before January 1st, 280. If you'd like, try ordering by ?BirthDate in the same way we ordered by ?Age.

### Why is this useful?

Imagine you have a dataset of registered voters in the united states that includes:

* Birth Date
* Party Affiliation

Using FILTER alongside SPARQL's grouping and aggregating features would allow you to determine the political lean of people born in a certain time frame.

### Exercise

When you're ready, try [this section's first exercise](./exercise_FYD_1.md).
