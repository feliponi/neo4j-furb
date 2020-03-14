# Neo4J 

Pós-DataScience - Neo4j

## Exercicíos 

Exercise 1.1: Retrieve all nodes from the database (Instructions)
```
MATCH (n) return n
```

### Exercise 1.2: Examine the data model of the graph (Instructions)

```
call db.schema.visualization()
```
### Exercise 1.3: Retrieve all Person nodes (Instructions)

```
match (p:Person) return p
```

### ### Exercise 1.4: Retrieve all Movie nodes (Instructions)

```
match (m:Movie) return m
```

Exercise 2.1: Retrieve all movies that were released in a specific year (Instructions)
Retrieve all Movie nodes that have a released property value of 2003.

```
match (m:Movie) where m.released = 2003 return m
```

### Exercise 2.2: View the retrieved results as a table (Instructions)
View the results you just viewed in Neo4j Browser as a table.

```
match (m:Movie {released:2003}) return m

m
{
  "title": "The Matrix Reloaded",
  "tagline": "Free your mind",
  "released": 2003
}
{
  "title": "The Matrix Revolutions",
  "tagline": "Everything that has a beginning has an end",
  "released": 2003
}

```

### Exercise 2.3: Query the database for all property keys (Instructions)

You want to know the existing property keys used in a graph. This will help you to write Cypher queries that utilizes property keys for filtering data or for returning data.

Query the database for all property keys.

```
call db.propertyKeys()

propertyKey
"tagline"
"title"
"released"
"born"
"name"
"roles"
"summary"
"rating"
```
### Exercise 2.4: Retrieve all Movies released in a specific year, returning their titles (Instructions)

Rather than returning the nodes that satisfy a query, you want to return data from the nodes.

Retrieve all Movies released in 2006, returning their titles.

```
match (m:Movie) where m.released = 2006 return m.title

m.title
"RescueDawn"
"The Da Vinci Code"
"V for Vendetta"
"RescueDawn"
"The Da Vinci Code"
"V for Vendetta"
```

### Exercise 2.5: Display title, released, and tagline values for every Movie node in the graph (Instructions)

When you start working with a graph, it is sometimes helpful to simply view property values. This can sometimes help to inform you about future queries you may want to execute against the graph.

Retrieve all Movie nodes from the database and return the title, released, and tagline values.

```
match (m:Movie) return m.title, m.tagline
```

### Exercise 2.6: Display more user-friendly headers in the table (Instructions)

Modify the query you just ran so that the headings for the columns of the table returned are more descriptive.

```
match (m:Movie) return m.title as 'Movie Title', m.released as 'Released', m.tagline as 'Tag Line'

```

### Exercise 3.1: Display the schema of the database (Instructions)

You will use schema information to help you specify relationships in your queries.

Display the schema of the database.

```
call db.schema.visualization()
```
### Exercise 3.2: Retrieve all people who wrote the movie Speed Racer (Instructions)

Retrieve all people who wrote the movie Speed Racer.
```
match(p:Person)-[:WROTE]->(:Movie {title: 'Speed Racer'}) return p.name
p.name
"Lana Wachowski"
"Lilly Wachowski"
"Lilly Wachowski"
"Lana Wachowski"
```
### Exercise 3.3: Retrieve all movies that are connected to the person, Tom Hanks (Instructions)

Retrieve all movies connected with Tom Hanks.

Hint: Tom Hanks has multiple relationships with a movie so you should not specify a relationship type in the query.

```
match(:Person {name: 'Tom Hanks'})-[:ACTED_IN]->(m:Movie) return m.title

m.title
"A League of Their Own"
"Cloud Atlas"
"The Da Vinci Code"
"Sleepless in Seattle"
"The Polar Express"
"The Green Mile"
"Cast Away"
"Charlie Wilson's War"
"That Thing You Do"
"Joe Versus the Volcano"
```

### Exercise 3.4: Retrieve information about the relationships Tom Hanks has with the set of movies retrieved earlier (Instructions)

Modify the query that you just executed to return the type information about the relationships between Tom Hanks and the movies.

```
match(:Person {name: 'Tom Hanks'})-[rel]-(m:Movie) return m.title, type(rel)

m.title	type(rel)
"A League of Their Own"	"ACTED_IN"
"Cloud Atlas"	"ACTED_IN"
"The Da Vinci Code"	"ACTED_IN"
"Sleepless in Seattle"	"ACTED_IN"
"The Polar Express"	"ACTED_IN"
"The Green Mile"	"ACTED_IN"
"Cast Away"	"ACTED_IN"

```

### Exercise 3.5: Retrieve information about the roles that Tom Hanks acted in (Instructions)

As an actor, a Person node in the database connects to a Movie node using the ACTED_IN relationship. One of the properties of the ACTED_IN relationship is roles.

Retrieve information about the roles that Tom Hanks played.

```
match(:Person {name: 'Tom Hanks'})-[r:ACTED_IN]->(m:Movie) return m.title, r.roles

m.title	r.roles
"A League of Their Own"	["Jimmy Dugan"]
"Cloud Atlas"	["Zachry", "Dr. Henry Goose", "Isaac Sachs", "Dermot Hoggins"]
"The Da Vinci Code"	["Dr. Robert Langdon"]
"Sleepless in Seattle"	["Sam Baldwin"]
"The Polar Express"	["Hero Boy", "Father", "Conductor", "Hobo", "Scrooge", "Santa Claus"]
"The Green Mile"	["Paul Edgecomb"]
```
### Exercise 4.1: Retrieve all movies that Tom Cruise acted in (Instructions)

Retrieve all movies that Tom Cruise acted in and return their titles.

Hint: Use a WHERE clause.

Hint: You must specify a variable for the Person and Movie nodes as they are used in the WHERE and RETURN clauses.

```
match (p:Person)-[:ACTED_IN]->(m:Movie) where p.name = 'Tom Cruise' return m.title
m.title
"Jerry Maguire"
"Top Gun"
"A Few Good Men"
"Top Gun"
"Jerry Maguire"
"A Few Good Men"
```
### Exercise 4.2: Retrieve all people that were born in the 70’s (Instructions)

Retrieve all people that were born in the 70’s and return their names and year born.

```
match(p:Person) where p.born >=1970 and p.born < 1980 return p.name

p.name
"Emil Eifrem"
"Charlize Theron"
"Noah Wyle"
"Jerry O'Connell"
"Jay Mohr"
"Regina King"
"River Phoenix"
"Corey Feldman"
```
### Exercise 4.3: Retrieve the actors who acted in the movie The Matrix who were born after 1960 (Instructions)

Retrieve the actors who acted in the movie The Matrix who were born after 1960, and return their names and year born.

```
match(p:Person)-[:ACTED_IN]->(m:Movie) where m.title = 'The Matrix' and p.born >=1960 return p.name

p.name
"Emil Eifrem"
"Laurence Fishburne"
"Hugo Weaving"
"Carrie-Anne Moss"
"Keanu Reeves"
"Hugo Weaving"
"Keanu Reeves"
"Emil Eifrem"
"Laurence Fishburne"
```
### Exercise 4.4: Retrieve all movies by testing the node label and a property (Instructions)

Retrieve all movies released in 2000 by testing the node label and the released property, returning the movie titles.

```
match(m) where m:Movie and  m.released = 2000 return m.title
m.title
"Jerry Maguire"
"The Replacements"
"Cast Away"
"Jerry Maguire"

```

### Exercise 4.5: Retrieve all people that wrote movies by testing the relationship between two nodes (Instructions)

Retrieve all people that wrote movies by testing the relationship between two nodes, returning the names of the people and the titles of the movies.

```
match(p:Person)-[rel]-(m:Movie) where type(rel) = 'WROTE'  return m.title, p.name
````

### Exercise 4.6: Retrieve all people in the graph that do not have a property (Instructions)

You will write Cypher queries using a WHERE clause to test existence.

Retrieve all people in the graph that do not have a born property, returning their names.

```
match(p:Person) where not exists(p.born) return p.name

p.name
"Naomie Harris"
"Paul Blythe"
"Angela Scope"
```

### Exercise 4.7: Retrieve all people related to movies where the relationship has a property (Instructions)

You will write Cypher queries using a WHERE clause to test existence.

Retrieve all people related to movies where the relationship has the rating property, then return their name, movie title, and the rating.

```
match(p:Person)-[rel]-(m:Movie) where exists(rel.rating) return p.name, m.title, rel.rating

p.name	m.title	rel.rating
"Jessica Thompson"	"Jerry Maguire"	92
"Angela Scope"	"The Replacements"	62
"James Thompson"	"The Replacements"	100
"Jessica Thompson"	"The Replacements"	65
```

### Exercise 4.8: Retrieve all actors whose name begins with James (Instructions)

Next you will practice queries that test string properties.

Retrieve all actors whose name begins with James, returning their names.

```
match(p:Person) where p.name starts with 'James' return p.name
p.name
"James Marshall"
"James L. Brooks"
"James Cromwell"
"James Thompson"
```
### Exercise 4.9: Retrieve all REVIEWED relationships from the graph with filtered results (Instructions)

Retrieve all REVIEWED relationships from the graph where the summary of the review contains the string fun, returning the movie title reviewed and the rating and summary of the relationship.

Hint: You do not know what case the fun string will be in the summary text.

```
match(p:Person)-[rel:REVIEWED]-(m:Movie) where rel.summary contains 'fun' return m.title, rel.rating, rel.summary

m.title	rel.rating	rel.summary
"The Replacements"	62	"Pretty funny at times"
"The Replacements"	65	"Silly, but fun"
"The Replacements"	62	"Pretty funny at times"
"The Replacements"	65	"Silly, but fun"
```

### Exercise 4.10: Retrieve all people who have produced a movie, but have not directed a movie (Instructions)

Next, you will write queries that test patterns.

Retrieve all people who have produced a movie, but have not directed a movie, returning their names and the movie titles.

```
match(p:Person)-[pr:PRODUCED]->(m:Movie) where not ((p)-[:DIRECTED]-(:Movie)) return p.name, m.title

p.name	m.title
"Joel Silver"	"The Matrix"
"Joel Silver"	"The Matrix Reloaded"
"Joel Silver"	"The Matrix Revolutions"
"Stefan Arndt"	"Cloud Atlas"
```
### Exercise 4.11: Retrieve the movies and their actors where one of the actors also directed the movie (Instructions)

Retrieve the movies and their actors where one of the actors also directed the movie, returning the actors names, the director’s name, and the movie title.

```
match(p:Person)-[rel]->(m:Movie) where ((p)-[:DIRECTED]-(:Movie)) and ((p)-[:ACTED_IN]-(:Movie)) return p.name, m.title

p.name	m.title
"James Marshall"	"Ninja Assassin"
"James Marshall"	"A Few Good Men"
"James Marshall"	"V for Vendetta"
"Werner Herzog"	"RescueDawn"
```

### Exercise 4.12: Retrieve all movies that were released in a set of years (Instructions)

Next you will perform queries using lists.

Retrieve all movies that were released in the years 2000, 2004, and 2008, returning their titles and release years.
```
MATCH (m:Movie)
WHERE m.released in [2000, 2004, 2008]
RETURN m.title, m.released

m.title	m.released
"Jerry Maguire"	2000
"The Replacements"	2000
"Speed Racer"	2008
```

### Exercise 4.13: Retrieve the movies that have an actor’s role that is the name of the movie (Instructions)

Retrieve the movies that have an actor’s role that is the name of the movie, return the movie title and the role.


```
match(p:Person)-[r:ACTED_IN]->(m:Movie) where m.title in r.roles return m.title, r.roles

m.title	r.roles
"Jerry Maguire"	["Jerry Maguire"]
"Johnny Mnemonic"	["Johnny Mnemonic"]
"Speed Racer"	["Speed Racer"]
"Hoffa"	["Hoffa"]
```
### Exercise 5.1: Retrieve data using multiple MATCH patterns (Instructions)

Write a Cypher query that retrieves all movies that Gene Hackman has acted it, along with the directors of the movies. In addition, retrieve the actors that acted in the same movies as Gene Hackman. Return the name of the movie, the name of the director, and the names of actors that worked with Gene Hackman.

```
match(p:Person)-[:ACTED_IN]->(m:Movie)<-[:DIRECTED]-(p2:Person), 
(p3:Person)-[:ACTED_IN]->(m) where p.name = 'Gene Hackman'
return m.title as Movie, p2.name as Director, p3.name As CoActors

Movie	Director	CoActors
"The Birdcage"	"Mike Nichols"	"Robin Williams"
"The Birdcage"	"Mike Nichols"	"Nathan Lane"
"The Replacements"	"Howard Deutch"	"Keanu Reeves"
"The Replacements"	"Howard Deutch"	"Orlando Jones"
"The Replacements"	"Howard Deutch"	"Brooke Langton"
"Unforgiven"	"Clint Eastwood"	"Richard Harris"
"Unforgiven"	"Clint Eastwood"	"Clint Eastwood"
"Unforgiven"	"Clint Eastwood"	"Clint Eastwood"
"Unforgiven"	"Clint Eastwood"	"Richard Harris"
```
### Exercise 5.2: Retrieve particular nodes that have a relationship (Instructions)

Next, you will perform queries for data that is a variable number of hops away.

Write this Cypher query to explore the graph engine’s behavior with varying length paths for the FOLLOWS relationship in the Movie graph:

Retrieve all nodes that the person named James Thompson directly has the FOLLOWS relationship in either direction.

```
match(p:Person)-[r:FOLLOWS]-(p2:Person)
where p.name = 'James Thompson'
return  p, p2
```

### Exercise 5.3: Modify the query to retrieve nodes that are exactly three hops away (Instructions)

Modify the query to retrieve nodes that are exactly three hops away.

```
match(p:Person)-[r:FOLLOWS*3]-(p2:Person)
where p.name = 'James Thompson'
return p, p2
```
### Exercise 5.4: Modify the query to retrieve nodes that are one and two hops away (Instructions)

Modify the query to retrieve nodes that are one and two hops away.

```
match(p:Person)-[r:FOLLOWS*1..2]-(p2:Person)
where p.name = 'James Thompson'
return p, p2

```

### Exercise 5.5: Modify the query to retrieve particular nodes that are connected no matter how many hops are required (Instructions)

Modify the query to retrieve all nodes that are connected to James Thompson by a Follows relationship no matter how many hops are required.

```
match(p:Person)-[r:FOLLOWS*]-(p2:Person)
where p.name = 'James Thompson'
return p, p2

p.name	p2.name
"James Thompson"	"Jessica Thompson"
"James Thompson"	"Angela Scope"
"James Thompson"	"Paul Blythe"
"James Thompson"	"Jessica Thompson"
"James Thompson"	"Angela Scope"
"James Thompson"	"Paul Blythe"
```

### Exercise 5.6: Specify optional data to be retrieved during the query (Instructions)

Write a Cypher query to retrieve all people in the graph whose name begins with Tom and optionally retrieve all people named Tom who directed a movie.

```
match(p:Person) 
where p.name starts with 'Tom'
optional match(p)-[:DIRECTED]-(m:Movie)
return p.name, m.title

p.name	m.title
"Tom Cruise"	null
"Tom Skerritt"	null
"Tom Hanks"	"That Thing You Do"
"Tom Tykwer"	"Cloud Atlas"

```


## Anotações

Todos os atores que performaram o papel de 'Neo' em todos os filmes do database

```
match (p)-[r:ACTED_IN]->(m) where p:Person and 'Neo' in r.roles and m:Movie return p.name, m.title

p.name	m.title
"Keanu Reeves"	"The Matrix"
"Keanu Reeves"	"The Matrix Reloaded"
"Keanu Reeves"	"The Matrix Revolutions"
"Keanu Reeves"	"The Matrix"
"Keanu Reeves"	"The Matrix Reloaded"
"Keanu Reeves"	"The Matrix Revolutions"

```
O relacionamento ACTED_IN também possui propriedades. Uma delas é o Roles.

