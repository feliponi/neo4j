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
#### Exercise 4.1: Retrieve all movies that Tom Cruise acted in

-Retrieve all movies that Tom Cruise acted in and return their titles.

```
MATCH (p:Person)-[r:ACTED_IN]->(m:Movie) WHERE p.name = 'Tom Cruise' RETURN m
```

#### Exercise 4.2: Retrieve all people that were born in the 70’s

```
MATCH (p:Person)  WHERE p.born >= 1970 and p.born < 1980 RETURN p.name, p.born
```

#### Exercise 4.3: Retrieve the actors who acted in the movie The Matrix who were born after 1960 

```
MATCH (p:Person)-[r:ACTED_IN]->(m:Movie) WHERE m.title = 'The Matrix' AND p.born > 1960  RETURN p.name, p.born
```

#### Exercise 4.4: Retrieve all movies by testing the node label and a property

```
MATCH (m) WHERE m:Movie AND m.released = 2000 RETURN m.title
```

#### Exercise 4.5: Retrieve all people that wrote movies by testing the relationship between two nodes

```
MATCH (a)-[rel]->(m) WHERE a:Person AND type(rel) = 'WROTE' AND m:Movie RETURN a.name, m.title
```

#### Exercise 4.6: Retrieve all people in the graph that do not have a property

```
MATCH (a:Person) WHERE NOT exists(a.born) RETURN a.name
```

#### Exercise 4.7: Retrieve all people related to movies where the relationship has a property

```
MATCH (a:Person)-[rel]->(m:Movie) WHERE exists(rel.roles) RETURN a.name as Name, m.title as Movie, rel.roles
```

#### Exercise 4.8: Retrieve all actors whose name begins with James

```
MATCH (a:Person)-[:ACTED_IN]->(:Movie) WHERE a.name STARTS WITH 'James'RETURN a.name
```

#### Exercise 4.9: Retrieve all REVIEWED relationships from the graph with filtered results

```
MATCH (:Person)-[r:REVIEWED]->(m:Movie) WHERE r.summary CONTAINS 'Fun' RETURN  m.title, r.summary, r.rating
```

#### Exercise 4.9: Retrieve all REVIEWED relationships from the graph where the summary of the review contains the string fun (Taking it further - optional)

- Retrieve all movies in the database that have love in their tagline and return the movie titles

```
MATCH (m:Movie) WHERE m.tagline CONTAINS 'love' RETURN  m.title
```

- Retrieve movies in the database, specifying a regular expression for the content of the tagline.

```
MATCH (m:Movie) WHERE m.tagline =~ '.*love.*' RETURN  m.title
```

#### Exercise 4.10: Retrieve all people who have produced a movie, but have not directed a movie

```
MATCH (a:Person)-[:PRODUCED]->(m:Movie) WHERE NOT ((a)-[:DIRECTED]->(:Movie)) RETURN a.name, m.title
```

#### Exercise 4.11: Retrieve the movies and their actors where one of the actors also directed the movie

```
MATCH (p1:Person)-[:ACTED_IN]->(m:Movie)<-[:ACTED_IN]-(p2:Person) WHERE exists((p2)-[:DIRECTED]->(m)) RETURN  p1.name, p2.name, m.title
```

#### Exercise 4.12: Retrieve all movies that were released in a set of years

```
MATCH (m:Movie) WHERE m.released in [2000, 2004, 2008] RETURN m.title, m.released
```

#### Exercise 4.13: Retrieve the movies that have an actor’s role that is the name of the movie

```
MATCH (a:Person)-[r:ACTED_IN]->(m:Movie) WHERE m.title in r.roles RETURN  m.title, a.name
```

#### Exercise 5.1: Retrieve data using multiple MATCH patterns

```

```










