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



