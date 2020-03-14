# neo4j-furb
Pós-DataScience - Neo4j

## Exercicíos 

Exercise 1.1: Retrieve all nodes from the database (Instructions)
```
MATCH (n) return n
```

Exercise 1.2: Examine the data model of the graph (Instructions)

```
call db.schema.visualization()
```
Exercise 1.3: Retrieve all Person nodes (Instructions)

```
match (p:Person) return p
```

Exercise 1.4: Retrieve all Movie nodes (Instructions)

```
match (m:Movie) return m
```

Exercise 2.1: Retrieve all movies that were released in a specific year (Instructions)
Retrieve all Movie nodes that have a released property value of 2003.

```
match (m:Movie) where m.released = 2003 return m
```

Exercise 2.2: View the retrieved results as a table (Instructions)
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

Exercise 2.3: Query the database for all property keys (Instructions)

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
Exercise 2.4: Retrieve all Movies released in a specific year, returning their titles (Instructions)

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

Exercise 2.5: Display title, released, and tagline values for every Movie node in the graph (Instructions)

When you start working with a graph, it is sometimes helpful to simply view property values. This can sometimes help to inform you about future queries you may want to execute against the graph.

Retrieve all Movie nodes from the database and return the title, released, and tagline values.

```
match (m:Movie) return m.title, m.tagline
```

Exercise 2.6: Display more user-friendly headers in the table (Instructions)

Modify the query you just ran so that the headings for the columns of the table returned are more descriptive.

```
match (m:Movie) return m.title as 'Movie Title', m.released as 'Released', m.tagline as 'Tag Line'

```

Exercise 3.1: Display the schema of the database (Instructions)

You will use schema information to help you specify relationships in your queries.

Display the schema of the database.

```
call db.schema.visualization()
```
Exercise 3.2: Retrieve all people who wrote the movie Speed Racer (Instructions)

Retrieve all people who wrote the movie Speed Racer.
```
match(p:Person)-[:WROTE]->(:Movie {title: 'Speed Racer'}) return p.name
p.name
"Lana Wachowski"
"Lilly Wachowski"
"Lilly Wachowski"
"Lana Wachowski"
```
Exercise 3.3: Retrieve all movies that are connected to the person, Tom Hanks (Instructions)

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

