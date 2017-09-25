# Sorting and Summary Statistics
Now we will cover a few more keywords and functions that help you get more out of your data. SPARQL has built-in methods for sorting and subsetting data. It also lets you find the minimum and maximum values of a particular property, as well as other common summary statistics like averages and sums.

## KEYWORDS you will learn in this tutorial

* ORDER BY - sorts the data
* LIMIT - retrieves a specific number of results
* MIN - returns the lowest value
* MAX - returns the highest value
* AVG - returns the average
* SUM - adds all the values
* COUNT - counts how many values there are

## Sorting Your Data
Use the **ORDER BY** key phrase after the WHERE section to sort data. For example, let's say instead of viewing the important people in our dataset organized by ID that we'd like to view them in alphabetical order by first name:

{% datadotworld "tutorial/sparqltutorial" %}
~~~~
PREFIX GOT: <https://tutorial.linked.data.world/d/sparqltutorial/>

SELECT ?FName ?LName

WHERE {
  ?person GOT:col-got-fname ?FName .
  ?person GOT:col-got-lname ?LName .
}
ORDER BY ?FName
  # Sorts data in alphabetical order by first name
~~~~
{% enddatadotworld %}

Try adding "**DESC**" to the "**ORDER BY**" phrase so it looks like `ORDER BY DESC (?LName)` and see what happens.

Next try `ORDER BY ?LName ?FName`, this will first order the results by last name, and then first name.

## Retrieving a specific number of results

Use the **LIMIT** keyword at the end of your query to return a specific number of results. For example, suppose you only wanted to see the first 5 records, just to get a sense of the data.

{% datadotworld "tutorial/sparqltutorial" %}
~~~~
PREFIX GOT: <https://tutorial.linked.data.world/d/sparqltutorial/>

SELECT ?ID ?FName ?LName

WHERE {
  ?person GOT:col-got-id ?ID .
  ?person GOT:col-got-fname ?FName .
  ?person GOT:col-got-lname ?LName .
}
LIMIT 5
~~~~
{% enddatadotworld %}

> ### NOTE
>
> The LIMIT keyword can be immensely helpful when your dataset has thousands of rows. Using LIMIT can also help decrease the compute time of your queries when testing whether they are returning the data you would like them to; it takes much longer to debug a query that is returning over 1 million rows than one that is limited to a fraction of that.

You can also combine "LIMIT 1" with "ORDER BY ..." and "ORDER BY DESC ..." to find the lowest and highest values in a dataset. Speaking of finding the lowest and highest values...

## Minima, Maxima, and Averages

Use the **MIN()** and **MAX()** functions within the SELECT portion of your query to return the lowest and highest value of the data, respectively. Something cool about the MIN() and MAX() functions is that they work on numerical values as well as strings, so returning the first FName from the data would look like this:

{% datadotworld "tutorial/sparqltutorial" %}
~~~~
PREFIX GOT: <https://tutorial.linked.data.world/d/sparqltutorial/>

SELECT (MIN(?FName) AS ?firstName)
  # Stores the minimum value bound to the ?FName variable in the ?firstName variable - only displays this value

WHERE {
  ?person GOT:col-got-fname ?FName .
}
~~~~
{% enddatadotworld %}

We've introduced some new syntax in the SELECT section with this query. What's going on here? The keyword **AS** divides the left and right side within the parentheses after SELECT, letting us set a *certain value* AS a *certain variable*.  For example, when we write

```
SELECT (MIN(?FName) AS ?firstName)
```

we are taking the MIN of the variable ?FName and *binding* that value to a new variable that we are calling ?firstName.

Take a look at the results. Notice how the property name is bound as "firstName" in the column header of the results? This is an indication that your binding using the MIN() function worked. Go ahead and try out MAX() too while you're at it.

Unlike MIN() and MAX(), **AVG()** is only valid for numerical values, so it will not work on strings. To find the average of all the ages in the data, you could use the following query:

{% datadotworld "tutorial/sparqltutorial" %}
~~~~
PREFIX GOT: <https://tutorial.linked.data.world/d/sparqltutorial/>

SELECT (AVG(?age) AS ?avgAge)
  # Stores the average of values bound to the ?age variablae in the ?avgAge variable - only displays this value

WHERE {
  ?person GOT:col-got-age ?age .
}
~~~~
{% enddatadotworld %}

Check out the results. Young crowd!

## Aggregations
Use **SUM()** and **COUNT()** to aggregate your data by value and by record. Here is an example of SUM():

{% datadotworld "tutorial/sparqltutorial" %}
~~~~
PREFIX GOT: <https://tutorial.linked.data.world/d/sparqltutorial/>

SELECT (SUM(?age) AS ?totalYears)
  # Stores the total of values bound to the ?age variable in the ?avgAge variable - only displays this value

WHERE {
  ?person GOT:col-got-age ?age .
}
~~~~
{% enddatadotworld %}

COUNT() can be very helpful in conjunction with AVG() and SUM(), because sometimes there will be missing data in your dataset. Three of the people in our dataset have no valid Age property value, so using COUNT() is a good practice to tell how many data points compose the other figures.

## Why is this useful?

Imagine putting inputting one simple query to find out the average age of left-leaning voters in a certain zipcode, or finding the heights of the 10 tallest NBA players. Sorting and aggregation makes that possible.

## Practice
Now you're ready for [the exercise](./exercise_SASS.md)!
