# Neo4j Timetabling Project

###### Author - Gary Mannion - G00319609
###### Module - Graph Theory
###### Lecturer - Ian McLoughlin

## Introduction  
My name is Gary Mannion and as part of a Graph Thoery Module based in GMIT I have to design and build a graph database using Neo4J and Cypher. Today Neo4J is the worlds most popular graph database managment system, it uses a language called Cypher as its query language.

The database I'm implementing is supposed to contain data regarding the GMIT timetable for my course. I must have data for Lecturers, rooms, course, module, day, times and groups. In this project I have implemented that data which I will be explaining in more detail later in this documentation.  

> Below is a screenshot of the current GMIT timetable for my course  
<img src="https://github.com/Gazza1996/Graph-Theory-Project/blob/master/readme%20images/Screenshot%20(6).png">  

## What is a Graph Database  
A graph database, also called a graph-oriented database, is a type of NoSQL database that uses graph theory to store, map and query relationships.   

A graph database is essentially a collection of nodes and edges. Each node represents an entity (such as a person or business) and each edge represents a connection or relationship between two nodes. Every node in a graph database is defined by a unique identifier, a set of outgoing edges and/or incoming edges and a set of properties expressed as key/value pairs. Each edge is defined by a unique identifier, a starting-place and/or ending-place node and a set of properties.  

> Below is an example of the nodes and edges being used to create a relatioship in the graph database  

<img src="http://itknowledgeexchange.techtarget.com/overheard/files/2014/01/Graph-database-sketch.jpg">  

## Neo4j and Cypher  

**Neo4j**  

Neo4j is a graph database management system developed by Neo Technology, Inc. Described by its developers as an ACID-compliant transactional database with native graph storage and processing, Neo4j is the most popular graph database.  

Neo4j is available in a GPL3-licensed open-source "community edition", with online backup and high availability extensions licensed under the terms of the Affero General Public License. Neo also licenses Neo4j with these extensions under closed-source commercial terms.  

Neo4j is implemented in Java and accessible from software written in other languages using the Cypher Query Language through a transactional HTTP endpoint, or through the binary 'bolt' protocol.  

Version 1.0 was released in February 2010.  

**Cypher**  

Cypher is a declarative, SQL-inspired language for describing patterns in graphs visually using an ascii-art syntax.  

It allows us to state what we want to select, insert, update or delete from our graph data without requiring us to describe exactly how to do it.  

> example of using cypher in a relationship

<img src="https://s3.amazonaws.com/dev.assets.neo4j.com/wp-content/uploads/cypher_pattern_simple.png">  

## Database  
Before i created my database I had to make a design decision on what part of the timetable to use.  
I decided to use the semester 2 of my course and use my exact timetable as the basis of the database.  
I then picked different nodes to incorporate the database. The nodes are listed as:  

```
1. Course
2. Lecturer
3. Rooms
4. Times
5. Days
6. Groups
```  
I added all 3 groups as nodes but only needed one(Group A) as that is my group.  

After selecting each node for the database i had to go and retrieve the data which consisted of me checking my timetable for the above properties which i placed into a textfile in the method needed to create them in the database which can be found in the repository.  

**Course**  
Here is how i created the node for my course name and details along with it.  
```
CREATE (SoftwareDevelopmentL7Yr3:Course{Name:"Software Development L7 Yr3 Sem2"})
```  
This is also an example of a cypher command.  

**Lecturer**  
For getting the information about lecturers i just got all the names for each module and created them like the example below
```
E.G,    CREATE (MartinHynes:Lecturers{Name:"Martin Hynes"})
```  

**Rooms**  
For getting the rooms I just took the rooms that are most used by the course and added them to the database.  
```
E.G,    CREATE (G0436CR5:Rooms{Name:"G0436 CR5"})
```

**Times**  
The times simply ranged from 9am until 6pm which I placed in hourly slots.  
```
Example: 
      CREATE (Slot1:Times{Name:"9am-10Am"})
      CREATE (Slot2:Times{Name:"10am-11Am"})
      CREATE (Slot3:Times{Name:"11am-12pm"})
      CREATE (Slot4:Times{Name:"12pm-1pm"})
```

**Days**  
The days are similar to Times as it ranges from Monday to Friday.  
```
Example:
            CREATE (Monday:Days{Name:"Monday"})
            CREATE (Tuesday:Days{Name:"Tuesday"})
```

**Groups**  
Added in the 3 groups in the course (A,B,C). However i only needed group A as that is my group for my timetable.  
```
E.G,        CREATE (GroupA:Groups{Name:"GroupA"})
```

## Relationship  
For creating a relationship between different nodes and properties proved to be very difficult and required a lot of research on the neo4j website and other websites which i have referenced.  

The way I designed my database through relationships was to join lecturers->Modules->Rooms->Times  
After this i would then join that Times->Days->Groups, or some cases if a class was 2 hours long i would make a relationship to a second time slot (UNTIL). Times->Times->Days->Groups.  

```
MATCH (a:Lecturers),(b:Module),(c:Rooms),(d:Times)
WHERE a.Name = 'Deirdre ODonovan' AND b.Name = 'Database Management Systems' AND c.Name = 'G0994' AND d.Name = '10am-11Am'
CREATE (a)-[r:TEACHES]->(b)
CREATE (b)-[r1:Lecture]->(c)
CREATE (c)-[r2:AT]->(d)
RETURN r,a,b,c,d

This command matches the lecturers,Modules,Rooms and Times and finds the properties named(Deirdre ODonovan)(Database Management Systems) etc. to make a relationship and then calling the relationship(TEACHES,LECTURE,AT) and will return the relationship and properties made.
```

I then did a second command to add extra relationships on this already created relationship.  
```
MATCH (a:Times),(b:Days)
WHERE a.Name = '10am-11Am' AND b.Name = 'Monday' 
CREATE (a)-[r:ON]->(b)
RETURN a,b,r 

This simply does the same as the previous command just takes the Times already in a relationship and adds the days to it(Monday) and creates the relationshipo(ON).
```

Finally, I decided that there should be a seperate relationship for the LAB time for all Modules that require lab times which i done inthe following way.  
```
MATCH (a:Module),(b:Rooms),(c:Times),(d:Times)
WHERE a.Name = 'Database Management Systems' AND b.Name = 'G0481 CR4' AND c.Name = '9am-10Am' AND d.Name = '10am-11Am'
CREATE (a)-[r:LAB]->(b)
CREATE (b)-[r1:AT]->(c)
CREATE (c)-[r2:UNTIL]->(d)
RETURN r,a,b,c,d

This command performs in the exact same way as the first example.
```

## Conclusion  
To summarize, graph databases like Neo4J and its supporting query language Cypher are becoming an increasingly popular tool today, especially in the last 10 years since social media has taken off. Facebook for example uses a graph database, this allows users to quickly search for their friends, friends of their friends and so on. I feel personally that in the future graph databases will only become increasingly popular and will be implemented in more and more environments. The use of the graph makes it very easy to the human eye to understand what nodes are within the database and also for relationships to know what is connected to each other and for what reason.  


## References  
- https://neo4j.com/docs/developer-manual/current/cypher/clauses/create/  
- http://whatis.techtarget.com/definition/graph-database
- https://www.tutorialspoint.com/graph_theory/  
- http://neo4j.com/developer/cypher
- http://neo4j.com/docs/stable/query-match.html
- http://timetable.gmit.ie/sws1617/(S(gudsqdfus0ilov45bqk3d2vi))/default.aspx
- https://neo4j.com/developer/cypher-query-language
- https://neo4j.com/docs/developer-manual/current/cypher/clauses/remove/
- https://neo4j.com/docs/developer-manual/current/cypher/clauses/match/
- https://neo4j.com/docs/developer-manual/current/cypher/clauses/where/
- https://neo4j.com/docs/developer-manual/current/cypher/clauses/delete/
- https://neo4j.com/docs/developer-manual/current/cypher/#cypher-intro
