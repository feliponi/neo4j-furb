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
