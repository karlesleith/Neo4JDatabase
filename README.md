# Neo4JDatabase
Neo4j database for use in a timetabling system for a third level institute like GMIT. To be submitted as Graph Theory Project due April 23rd 2017.

## Author
**Karle Sleith**

## Purpose
The purpose of this assignment is to create a protoype database, using data from GMIT. The database
should store information about student groups, classrooms, lecturers, and
work hours. 

## Design

![Screenshot](Design.png)

The idea for the design was to use a tree hirearchy, with the Day being the root. I had to ask the questions, whats the MAX hours in a school day, what classes are on at what time?, who's in thoses classes? ect, with that I was able to come up with a basic design for my Database.

## Implementation
I decided that the best way to keep track of what I was doing was to use simple .txt files that I would write the syntax in, then copy the information into my Neo4J Database, I made a text file for each year in Software Devleopment, starting with my own year, Year 3.

To find the data I needed for my DataBase, I scraped the Room Information from <a href="http://timetable.gmit.ie">http://timetable.gmit.ie/<a/>, after which I removed the unnecessary code, and replaced it with my own Using "Find and Replace" to allow me to make Nodes for every room in one long command, after I was done I Created the adddional nodes I needed one by one; Lecturers, Course, Year, Day, TimeSlot. 

![Screenshot2](Code.PNG)

After creating the Nodes, I continued to create the relationships between, I created a syntax template and was able to replace the information as needed to create the connected Database.

When I was finished I deleted the remaining room nodes that had no relationships.

![Screenshot3](Graph.PNG)

## How To Use the Database

### Query 1
Here I'm looking to find what modules the Lecturer "Ian McLoughlin" teaches, to do that I'll use this syntax:

 **match (n: Lecturer{name: 'Ian McLoughlin'}) -[*..2]-(Year)
return DISTINCT n, Year**

Above I'm looking to see how the node for "Ian McLoughlin" relates to any node of type "Year", the "*..2" refers to the depth of my query from my starting node.

![Query1](Query.PNG)

My Result ended up looking like this.
The node "Ian" is at the center and the path it will take away from him, is 2 levels deep.

### Query 2

Now I want to find the shorest path between the nodes for "Ian McLoughlin" and "Martin Hynes"

**match p =ShortestPath((n: Lecturer{name: 'Ian McLoughlin'}) -[*]- (b: Lecturer{name: 'Martin Hynes'}))
return p** 

![Query2](Query2.PNG)

It shows they both have a lecture on in room "G0223", and thats what connects them together.


### Query 3

Finally what if i want to see all the nodes that relate to Graph Theory?

**match (n: Module{name: 'Graph Theory'}) -[*..2]-(course)
return DISTINCT n, course**

![Query3](Query3.PNG)



