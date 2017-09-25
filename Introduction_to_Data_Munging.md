#Introduction to Data Munging
If you would like to modify your datasets to produce new results, you might want to create variables and give them values. We've already covered this somewhat in "Wrangling Your Data", but what if you want to filter on variables that you have bound values to?

##KEYWORDS and concepts you will learn:
* BIND - binding a value to a variable
* Filtering variables that you have bound
* MONTH - returns the month from a date value.
* CONCAT - concatenate strings together
* STRLEN - find the length of strings

### BIND

SPARQL's BIND function allows us to assign a value to a variable. It looks like this:

```
BIND (MONTH(?birthDate) AS ?birthMonth)
```

The left side **[month(?birthDate)]** is where we set the value of our variable, the right side **[?birthMonth]** is where we define the variable. The keyword AS separates the two sides. Notice this looks the same as the binding we did using the SELECT keyword in "Wrangling Your Data". The key difference is the binding is done within the WHERE section of the query.

In this case, we are using the SPARQL function MONTH to grab the month out of each character's birth date, and then we are assigning this value to ?birthMonth. Here's what it looks like as a full SPARQL query:

{% raw  %}
~~~~
PREFIX GOT: <https://tutorial.linked.data.world/d/sparqltutorial/>

SELECT ?FName ?LName ?birthMonth

WHERE {
	?person GOT:col-got-fname ?FName ;
        	GOT:col-got-lname ?LName ;
        	GOT:col-got-birthdate ?birthDate .
	BIND (MONTH(?birthDate) AS ?birthMonth)
}
~~~~
{% endraw  %}

This returns a table of the birth months of each character in our dataset.

###FILTER and BIND

So why is BIND useful? Well we can now run SPARQL's FILTER function on ?birthMonth. Let's filter for characters born in February:

{% raw  %}
~~~~
PREFIX GOT: <https://tutorial.linked.data.world/d/sparqltutorial/>

SELECT ?FName ?LName ?birthMonth

WHERE {
	?person GOT:col-got-fname ?FName ;
        	GOT:col-got-lname ?LName ;
        	GOT:col-got-birthdate ?birthDate .
	BIND (MONTH(?birthDate) AS ?birthMonth)
	FILTER(?birthMonth = 2)
}
~~~~
{% endraw  %}

Neat, right?

###Using SPARQL filter and aggregate functions with FILTER and BIND

Let's try using this in conjunction with the SPARQL's string concatenation function CONCAT. Here's how it looks:

```
BIND (CONCAT(?FName, " ", ?LName) AS ?name)
```

With this one line, we've concatenated the first name, a space, and the last name together, and assigned it to the variable ?name. So ["Tyrion", " ", "Lannister"] becomes ["Tyrion Lannister"].

Now let's try filtering for full names longer than 12 characters. We can do this by using SPARQL's STRLEN function, which determines the length of strings.

{% raw  %}
~~~~
PREFIX GOT: <https://tutorial.linked.data.world/d/sparqltutorial/>

SELECT ?name

WHERE {
	?person GOT:col-got-fname ?FName ;
        	GOT:col-got-lname ?LName ;
	BIND (CONCAT(?FName, " ", ?LName) AS ?name)
    FILTER (STRLEN(?name) > 12)
}
~~~~
{% endraw  %}

### Why is this useful?

What if you had a dataset of football players that included their birth date. By using FILTER, BIND, and SPARQL's MONTH function you could start creating data on what month these players are born in. Add in SPARQL's COUNT and SUM functions and you're well on the way to finding out if there are any interesting correlations or trends for birth months of football players (Spoiler alert: [there are](http://www.footballperspective.com/does-when-you-were-born-impact-your-chances-of-making-the-nfl/).)

### Exercise

Now let's try [the exercise](./exercise_IDM.md).
