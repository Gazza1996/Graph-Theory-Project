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

## Relationship

## Conclusion  



## References  
- (https://neo4j.com/docs/developer-manual/current/cypher/clauses/create/)  
- (http://whatis.techtarget.com/definition/graph-database)
