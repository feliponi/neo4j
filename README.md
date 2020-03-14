#### Exercise 1.1: Retrieve all nodes from the database

```
MATCH (n) RETURN n
```

#### Exercise 1.2: Examine the schema of your database

```
call db.schema.visualization
```

#### Exercise 1.3: Retrieve all Person nodes

```
MATCH (p:Person) return p
```

#### Exercise 1.4: Retrieve all Movie nodes

```
MATCH (m:Movie) return m
```

#### Exercise 2.1: Retrieve all movies that were released in a specific year

```
MATCH (m:Movie {released: 2003}) RETURN m
```

#### Exercise 2.2: View the retrieved results as a table

```
MATCH (m:Movie {released: 2003}) RETURN m.title, m.released, m.tagline
```

#### Exercise 2.3: Query the database for all property keys

```
call db.propertyKeys
```

#### Exercise 2.4: Retrieve all Movies released in a specific year, returning their titles

```
MATCH (m:Movie {released: 2006}) RETURN m.title
```

#### Exercise 2.4: Retrieve all Movies released in a specific year, returning their titles

```
MATCH (m:Movie {released: 2004}) RETURN m.title, m.tagline, m.released
```

#### Exercise 2.5: Display title, released, and tagline values for every Movie node in the graph

```
MATCH (m:Movie) RETURN m.title, m.tagline, m.released
```

#### Exercise 2.6: Display more user-friendly headers in the table

```
MATCH (m:Movie) RETURN m.title as titulo, m.tagline as tag, m.released as datalancamento
```

#### Exercise 3.1: Display the schema of the database

```
call db.schema.visualization
```

### Exercise 3.2: Retrieve all people who wrote the movie Speed Racer

```
MATCH (p:Person)-[rel:WROTE]->(m:Movie { title: 'Speed Racer'}) RETURN p.name, rel, m.name
```

#### Exercise 3.2: Retrieve all people who wrote the movie Speed Racer
-Retrieve all people who have written other movies.  
-Retrieve people who have acted in a particular movie.  
-Retrieve people who have directed a particular movie.  

```
MATCH (p:Person)-[rel:WROTE]->(m:Movie { title: 'A Few Good Men'})
RETURN p, rel, m
```
```
MATCH (p:Person)-[rel:ACTED_IN]->(m:Movie { title: 'Speed Racer'})
RETURN p, rel, m
```
```
MATCH (p:Person)-[rel:DIRECTED]->(m:Movie { title: 'Speed Racer'})
RETURN p, rel, m
```
#### Exercise 3.3: Retrieve all movies that are connected to the person, Tom Hanks

```
MATCH (p:Person {name: 'Tom Hanks'})-[rel]->(m:Movie)
RETURN p, rel, m
```

#### Exercise 3.3: Retrieve all movies that are connected to the person, Tom Hanks
-Retrieve all movies connected with another actor.  
-Retrieve all people connected with a particular movie. 

```
MATCH (p:Person {name: 'Tom Cruise'})-[rel]->(m:Movie)
RETURN p, rel, m
```
```
MATCH (p:Person)-[rel]->(m:Movie {title: 'The Matrix'})
RETURN p, rel, m
```

#### Exercise 3.4: Retrieve information about the relationships Tom Hanks has with the set of movies retrieved earlier

```
MATCH (p:Person {name: 'Tom Hanks'})-[rel]->(m:Movie)
RETURN type(rel)
```

-Retrieve the relationship information about a different actor.  

```
MATCH (p:Person {name: 'Tom Cruise'})-[rel]->(m:Movie)
RETURN type(rel)
```
#### Exercise 3.5: Retrieve information about the roles that Tom Hanks acted in

```
MATCH (p:Person {name: 'Tom Hanks'})-[r:ACTED_IN]->(m:Movie)
RETURN p.name, r.roles
```

-Retrieve all roles for a different actor.  

```
MATCH (p:Person {name: 'Tom Cruise'})-[r:ACTED_IN]->(m:Movie)
RETURN m.title, r.roles
```

-Retrieve all roles played for a particular movie.  

```
MATCH (p:Person {name: 'Tom Cruise'})-[r:ACTED_IN]->(m:Movie)
RETURN m.title, r.roles
```
