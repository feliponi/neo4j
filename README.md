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
MATCH (p1:Person)-[:ACTED_IN]->(m:Movie)<-[:DIRECTED]-(p2:Person), (p3:Person)-[:ACTED_IN]->(m) WHERE p1.name = 'Gene Hackman'
RETURN m.title, p2.name , p3.name
```

#### Exercise 5.2: Retrieve particular nodes that have a relationship

```
MATCH (p1:Person)-[:FOLLOWS]-(p2:Person) WHERE p1.name = 'James Thompson' RETURN p1, p2
```

#### Exercise 5.3: Modify the query to retrieve nodes that are exactly three hops away

```
MATCH (p1:Person)-[:FOLLOWS*3]-(p2:Person) WHERE p1.name = 'James Thompson' RETURN p1, p2
```

#### Exercise 5.4: Modify the query to retrieve nodes that are one and two hops away

```
MATCH (p1:Person)-[:FOLLOWS*1..2]-(p2:Person) WHERE p1.name = 'James Thompson' RETURN p1, p2
```

#### Exercise 5.5: Modify the query to retrieve particular nodes that are connected no matter how many hops are required

```
MATCH (p1:Person)-[:FOLLOWS*]-(p2:Person) WHERE p1.name = 'James Thompson' RETURN p1, p2
```

#### Exercise 5.6: Specify optional data to be retrieved during the query 

```
MATCH (p:Person) WHERE p.name STARTS WITH 'Tom' OPTIONAL MATCH (p)-[:DIRECTED]->(m:Movie) RETURN p.name, m.title
```

#### Exercise 5.7: Retrieve nodes by collecting a list

```
MATCH (p:Person)-[:ACTED_IN]->(m:Movie) RETURN p.name as actor, collect(m.title)
```

#### xercise 5.8: Retrieve all movies that Tom Cruise has acted in and the co-actors that acted in the same movie by collecting a list

```
MATCH (p:Person)-[:ACTED_IN]->(m:Movie)<-[:ACTED_IN]-(p2:Person) WHERE p.name ='Tom Cruise' RETURN m.title as movie, collect(p2.name) 
```

#### Exercise 5.9: Retrieve nodes as lists and return data associated with the corresponding lists 

```
MATCH (p:Person)-[:REVIEWED]->(m:Movie) RETURN m.title as movie, count(p) as numReviews, collect(p.name) as reviewers
```

#### Exercise 5.10: Retrieve nodes and their relationships as list

```
MATCH (d:Person)-[:DIRECTED]->(m:Movie)<-[:ACTED_IN]-(a:Person) RETURN d.name AS director, count(a) AS `number actors` , collect(a.name) AS `actors worked with`
```

#### Exercise 5.11: Retrieve the actors who have acted in exactly five movies

```
MATCH (a:Person)-[:ACTED_IN]->(m:Movie) WITH  a, count(a) AS numMovies, collect(m.title) AS movies WHERE numMovies = 5
RETURN a.name, movies
```

#### Exercise 5.12: Retrieve the movies that have at least 2 directors with other optional data

```
MATCH (m:Movie) WITH m, size((:Person)-[:DIRECTED]->(m)) AS directors WHERE directors >= 2 OPTIONAL MATCH (p:Person)-[:REVIEWED]->(m) RETURN  m.title, p.name
```

#### Exercise 6.1: Execute a query that returns duplicate records.

```
MATCH (a:Person)-[:ACTED_IN]->(m:Movie) WHERE m.released >= 1990 AND m.released < 2000 RETURN DISTINCT m.released, m.title, collect(a.name)
```

#### Exercise 6.2: Modify the query to eliminate duplication

```
MATCH (a:Person)-[:ACTED_IN]->(m:Movie) WHERE m.released >= 1990 AND m.released < 2000 RETURN  m.released, collect(m.title), collect(a.name)
```

#### Exercise 6.3: Modify the query to eliminate more duplication.

```
MATCH (a:Person)-[:ACTED_IN]->(m:Movie) WHERE m.released >= 1990 AND m.released < 2000 RETURN  m.released, collect(DISTINCT m.title), collect(a.name)
```

#### Exercise 6.4: Sort results returned

```
MATCH (a:Person)-[:ACTED_IN]->(m:Movie) WHERE m.released >= 1990 AND m.released < 2000 RETURN  m.released, collect(DISTINCT m.title), collect(a.name) ORDER BY m.released DESC
```

#### Exercise 6.5: Retrieve the top 5 ratings and their associated movies

```
MATCH (:Person)-[r:REVIEWED]->(m:Movie) RETURN  m.title AS movie, r.rating AS rating ORDER BY r.rating DESC LIMIT 5
```

#### Exercise 6.6: Retrieve all actors that have not appeared in more than 3 movies

```
MATCH (a:Person)-[:ACTED_IN]->(m:Movie) WITH  a,  count(a) AS numMovies, collect(m.title) AS movies WHERE numMovies <= 3
RETURN a.name, movies
```

#### Exercise 7.1: Collect and use lists

Write a Cypher query that retrieves all actors that acted in movies, and also retrieves the producers for those movies. During the query, collect the names of the actors and the names of the producers. Return the movie titles, along with the list of actors for each movie, and the list of producers for each movie making sure there is no duplication of data. Order the results returned based upon the size of the list of actors.

```
MATCH (a:Person)-[:ACTED_IN]->(m:Movie), (m)<-[:PRODUCED]-(p:Person) WITH  m, collect(DISTINCT a.name) AS cast, collect(DISTINCT p.name) AS producers RETURN DISTINCT m.title, cast, producers ORDER BY size(cast)
```

#### Exercise 7.2: Collect a list

Write a Cypher query that retrieves all actors that acted in movies, and collects the list of movies for any actor that acted in more than five movies. Return the name of the actor and the list.

```
MATCH (p:Person)-[:ACTED_IN]->(m:Movie) WITH p, collect(m) AS movies WHERE size(movies) > 5 RETURN p.name, movies
```

#### Exercise 7.3: Unwind a list

Modify the query you just wrote so that before the query processing ends, you unwind the list of movies and then return the name of the actor and the title of the associated movie.

```
MATCH (p:Person)-[:ACTED_IN]->(m:Movie) WITH p, collect(m) AS movies WHERE size(movies) > 5 WITH p, movies UNWIND movies AS movie RETURN p.name, movie.title
```

#### Exercise 7.4: Perform a calculation with the date type

Write a query that retrieves all movies that Tom Hanks acted in, returning the title of the movie, the year the movie was released, the number of years ago that the movie was released, and the age of Tom when the movie was released.

```
MATCH (a:Person)-[:ACTED_IN]->(m:Movie) WHERE a.name = 'Tom Hanks' RETURN  m.title, m.released, date().year  - m.released as yearsAgoReleased, m.released  - a.born AS `age of Tom` ORDER BY yearsAgoReleased
```

#### Exercise 8.1: Create a Movie node

Create a Movie node for the movie with the title, Forrest Gump.

```
CREATE (:Movie {title: 'Forrest Gump'})
```

#### Exercise 8.2: Retrieve the newly-created node

Retrieve the node you just created by its title.

```
MATCH (m:Movie) WHERE m.title = 'Forrest Gump' RETURN m
```

#### Exercise 8.3: Create a Person node

Create a Person node for the person with the name, Robin Wright.

```
CREATE (:Person {name: 'Robin Wright'})
```

#### Exercise 8.4: Retrieve the Person node you just created by its name

Retrieve the Person node you just created by its name.

```
MATCH (p:Person) WHERE p.name = 'Robin Wright' RETURN p
```

#### Exercise 8.5: Add a label to a node

Add the label OlderMovie to any Movie node that was released before 2010.

```
MATCH (m:Movie) WHERE m.released < 2010 SET m:OlderMovie RETURN DISTINCT labels(m)
```

#### Exercise 8.6: Retrieve the node using the new label

Retrieve all older movie nodes to test that the label was indeed added to these nodes.

```
MATCH (m:OlderMovie) RETURN m.title, m.released
```

#### Exercise 8.7: Add the Female label to selected nodes (Instructions)

Add the label Female to all Person nodes that has a person whose name starts with Robin.

```
```




