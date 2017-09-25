# List of SPARQL Filter Functions

* Logical: !, &&, ||
 * ! - not, negation
 * Example: (!true) is the same as false
 * &&: and
 * Example: (?age > 10 && ?age < 15) includes anyone in the age range from 10-15.
 * ||: or
 * Example: (?age < 10 || ?age > 15) includes anyone younger than 10 or older than 15
* Math: +, -, *, /
 * +: addition
 * -: subtraction
 * *: multiplication
 * /: division
* Comparison: =, !=, >, <, IN, NOT IN...
 * =: is equal to
 * !=: is not equal to
 * \>, <; greater than and less than
 * IN, NOT IN: determine if an item is or is not in a set
 * Example: (?Ford IN ?cars) should hopefully return true
* SPARQL tests: isIRI, isURI, isBlank, isLiteral, isNumeric, bound
 * isIRI, isURI: returns true if the term is an IRI or a URI
 * isBlank: returns true if the term is a blank node
 * isLiteral: returns true if the term is a literal
 * isNumeric: returns true if the term is a numeric value
 * bound: returns true if a variable is assigned a value (INF or infinite, and NaN or not a number are considered valid values)
* SPARQL accessors: str, lang, datatype
* Other: sameTerm, langMatches, regex, REPLACE
* Conditionals: IF, COALESCE, EXISTS, NOT EXISTS
* Constructors: URI, BNODE, STRDT, STRLANG, UUID, STRUUID
* Strings: STRLEN, SUBSTR, UCASE, LCASE, STRSTARTS, STRENDS, CONTAINS, STRBEFORE, STRAFTER, CONCAT, ENCODE_FOR_URI
* More math: abs, round, ceil, floor, RAND
* Date/time: now, year, month, day, hours, minutes, seconds, timezone, tz
* Hashing: MD5, SHA1, SHA256, SHA384, SHA512




