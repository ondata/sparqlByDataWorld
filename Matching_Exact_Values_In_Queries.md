# Matching Exact Values In Queries

In the last section, you learned how to return a lot of data at once with variables. That approach is good when first exploring a dataset to show, for example, all resources' first and last names.

But what if you want to find a specific subset or entry of the data that contains specific values? Let's do that.

## KEYWORDS and concepts you'll learn
* Literals - words of 0 or more characters within double quotation marks ("", "foo", "bar", "SPARQL", etc.)
* OPTIONAL - searches for data that might not exist in the dataset

## Searching for Strings
### Literals
The below query contains new syntax in the form of a "literal," which is a fancy way of saying "an exact word or phrase within quotes." Let's say we know there is a person in the dataset with the exact first name "Daenerys" and we want to get her bio info:

{% raw  %}
~~~~
PREFIX GOT: <https://tutorial.linked.data.world/d/sparqltutorial/>

SELECT ?FName ?LName ?House ?Age

WHERE
{
    ?person GOT:col-got-fname "Daenerys" .
    ?person GOT:col-got-fname ?FName .
    ?person GOT:col-got-lname ?LName .
    ?person GOT:col-got-house ?House .
    ?person GOT:col-got-age ?Age .
}
~~~~
{% endraw  %}

This query first searches for a resource with an FName property with value "Daenerys". In this case, "Daenerys" is a string and must be denoted with quotes in the form of a literal for the SPARQL processor to recognize it. Once the processor finds the resource, the rest of the statements bind the appropriate values to the variables `?FName`, `?LName`, `?House`, and `?Age`.

Notice how we needed two lines that begin with `?person GOT:col-got-fname`, one for the literal "Daenerys" and one for the `?FName` variable? Why do you suppose that is? Try removing the line `?person GOT:col-got-fname ?FName` from this code, then running the query again.

This query may have told the SPARQL processor to look for the resource with "Daenerys" in the FName property and even SELECTed an `?FName` variable, but unless we explicitly bind a value to the `?FName` variable in a statement, the query will return nothing for that property.

## Searching for Numerical Values
Unlike strings, numerical values like integers and doubles do not require quotes for the SPARQL processor to recognize them. For example, let's say we wanted to search for all characters who are 34 years old:

{% raw  %}
~~~~
PREFIX GOT: <https://tutorial.linked.data.world/d/sparqltutorial/>

SELECT ?FName ?LName ?House ?Age

WHERE
{
    ?person GOT:col-got-age 34 .
    ?person GOT:col-got-fname ?FName .
    ?person GOT:col-got-lname ?LName .
    ?person GOT:col-got-house ?House .
    ?person GOT:col-got-age ?Age .
}
~~~~
{% endraw  %}

SPARQL has many more data types like dates and booleans, you'll learn about these later in this tutorial.

## Searching for Data That Might Not Exist
Many datasets have missing values, and basic SPARQL queries will only return data when the pattern in the WHERE section *exactly* matches the pattern in the data you're querying. This is because SPARQL is a *pattern-matching* query language. Data is only a match for the query if there is valid data in each piece of the statement declared within WHERE. This means SPARQL will return nothing when the data resource has a missing property name or value requested in WHERE. For example, try this query with which we want to show resources' IDs, first names, and ages.

{% raw  %}
~~~~
PREFIX GOT: <https://tutorial.linked.data.world/d/sparqltutorial/>

SELECT ?ID ?FName ?Age

WHERE {
  ?person GOT:col-got-id ?ID .
  ?person GOT:col-got-fname ?FName .
  ?person GOT:col-got-age ?Age .
}
~~~~
{% endraw  %}

As you can see, only the resources with valid property values for all three property names are listed, and unfortunately, some of our famous people do not have valid age values... Sorry, Robb, Viserys, and Rhaegar.

Use the OPTIONAL keyword within the WHERE section to denote optional patterns you'd like to match in the data. In other words, OPTIONAL allows you to search for data that may or may not be there! Try changing the line `?person GOT:col-got-age ?Age .` to `OPTIONAL { ?person GOT:col-got-age ?Age } .` to see Robb, Viserys, and Rheagar in the data.

## Why is this useful?

These queries give you a fast, effective way to grab pieces of data. Even cooler, you can directly download the data that you `SELECT` with these queries using [data.world](https://data.world). Imagine you have all the census data, and you only want to get the data on people in the age range of 20-30 who live in California and are school teachers. With a simple query, you can `SELECT` all this data and immediately download it, instead of having to download the entire massive data file.

## Practice
Now you're ready for [the exercise](./exercise_MEVIQ.md)!
