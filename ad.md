XML
1. motivation: to have one language to speak about data
XML is a Data Exchange Format
->XML = data + structure(mark-up)
->ordinary text files
->brackets describe a tree structure(actually graph stuctures)
->allows applications from different vendors to exchange data!
->standardized, extremely widely accepted!
Problem: highly verbose, lots of repetitive markup
PRO: we hava a standard
XML Type definition language such as DTD, XML Schema, or Relax NG
DTD(Document Type Description): element names and their content
->element
->text 
->attributes <entry date=“2017-01-16”> at most one date-attribute / no substructure possible
->processing instructions <?php sql ()..?> intended to carry instructions to the application
->comments <!-- some comment -->
->namespaces Namespaces provide unique element and attribute names <edi:price xmlns:edi='http://ecommerce.org/schema' units='Euro'>32.18</edi:price>
->entity references(two kinds) character reference Type <key>less-than</key> (&#x3C;) to save options.
XML: not tree but graph
attributes of type ID: must be unique
may be referenced via attributes of type IDREF
XML 
yes: has become very popular and adopted
no: standard too complex/ causes eg. slowness of XML parsers
XML vs JSON
xml: 7 node types/ DTDs are built in / very rich schema lanugaes, e.g. XML Schema
JSON: 6 data types: -number -string -boolean -array -object -empty value(null)
2. well-formed XML
A textual object is well-formed XML if,
(1) taken as a whole, it matches the production labled document
(2) it meets all the well-formedness constraines given in this specification
document = start-symbol of a context-free grammar(XML grammar)
XML Grammar - EBNF-style
->DTD is part of XML
-> DTDs may contain (deterministic) regular expressions
->How expensive is it to match a text of size n against a regular expression of size m?
-> DTDs allow recursive definitions
-> DTDs allow ID and IDREF attributes
XML vs JSON
->XML has advantages over JSON as a markup language
->JSON is less verbose than XML & naturally represents objects/arrays
parsing/DTD Validation: Introduction
3.DTD(Document type definitions)
->DTD may appear at the beginning of an XML document
->or be included from a file: <!DOCTYPE xyz SYSTEM "xyz.dtd">
(1) Entity declarations <!ENTITY hi “Hello”> <greeting>&hi; World!</greeting>
(2) Attribute-list declarations  <!ATTLIST person securityNumber CDATA #REQUIRED>
(3) Element type declarations <!ELEMENT friend (name,affil*,email*)>
(4) Notation declarations <!NOTATION jpg PUBLIC "JPG 1.0" "image/jpeg">

2. Attribute-list declarations
(1) fixed default attribute values
<!ATTLIST element-name attribute-name attribute-type #FIXED "value">
(2) variable attribute value(with default)
<!ATTLIST element-name attribute-name attribute-type "value">
(3) Enumerated attribute type
<!ATTLIST element-name attribute-name (value1|value2|..) “value”>
(4) Required attribute
<!ATTLIST element-name attribute_name attribute-type #REQUIRED>

3. Element Type Declarations
<!ELEMENT element-name content-model>
content models:
→ EMPTY – no content is allowed
→ ANY – any content is allowed
→ (#PCDATA | element-name | ...)* - “mixed content” , arbitrary sequence of character data and listed elements
→ deterministic regular expression over element names - sequence of elements
matching the expression
- choice: (...|...|...|...)
- sequence (...,...,...)
- optional:...?
- zero or more: ...* 
- one or more: ...+

  Mixed Content
mixed content is described by a repearable or group (#PCDATA | element-name | ...)*

-  Inside the group, no regular expressions – just element names
- #PCDATA must be first, followed by 0 or more element names that are separated by |
- The group can be repeated 0 or more times

Regular Expressions are ubiquitous in computer science!  used in EBNF, for defining the syntax of PLs
-> used in various unix tools (e.g., grep, ed)
-> supported in most PLs (esp. Perl), text editors
-> classical concept in CS (Stephen Kleene, 1950’s)


Finite-State Automata (FA) even more useful concept!
-> constant memory computation.
-> as Turing Machines, but read-only and one-way (left-to-right)  for every ReEx there is a FA (and vice versa)
-> useful in many areas of CS (verification, compilers, learning, hardware, linguistics, UML, etc )

Deterministic FA (DFA) = no two outgoing edges with same label
DFA Matching: time O( |w| )
“only one finger needed”
FA Matching: time O( |FA| * |w| )
“only at most #states-many fingers needed”

-> every FA can be effectively transformed into an equivalent DFA. 
-> can take exponential time!

BuildFA(e) = “Glushkov Automaton” = “Position Automaton” [Glushkov1961]
BuildFA(e) = every letter in e becomes a state

The XML specification restricts regular expressions in DTDs to be deterministic (1-unambiguous)
Unambiguous regular expression: “each word is witnessed by at most one sequence of positions of symbols in the expression that matches the word“ .[Brüggemann-Klein, Wood 1998]

->there exist regular expressions for which no equivalent deterministic expression exists

XML Parsers
-> Document Object Model -DOM : complex applications, XSLT, editor
-> Simple API for XML -SAX: simple applications, very efficient

DOM - loads full document into memory
SAX - generates streaming events
    - by default: nothing stored in memory

DOM 
-> Language and platform-independent view of XML
-> DOM APIs exist for many PLs (Java, C++, C, Python, JavaScript ...)
DOM relies on two main concepts
(1) The XML processor constructs the complete XML document tree (in-memory)
(2) The XML application issues DOM library calls to explore and manipulate the XML tree, or to generate new XML trees.

Advantages
• easy to use
• once in memory, no tricky issues with XML syntax anymore
• all DOM trees serialize to well-formed XML (even after arbitrary updates)!
Disadvantage Uses LOTS of memory!!
XML size
81M x2->164M Text only, with one embracing element
52M x13->680M Treebank, deep tree structure, short tagnames


SAX - Simple API for XML
SAX processors use constant space, regardless of the XML input document size. (not entirely correct: space proportional to document depth)

A SAX processor reads its input document sequentially and once only
no memory of what the parser has seen so far is retained while parsing. 

startDocumnet <?xml ...?>
endDocumnet <EOF>
startElement <t a=v>
endElement </t>
characters text content (characters of one text node may be sent in several chunks)
comment <!--c-->
processiongInstribution <?t pi?>

Data Redundancy Problem
->Data redundancy leads to data anomalies and corruption
->Data redundancy should be avoided by design!

Issue with the ID/IDREF solution:
->Where are UserID-entries kept in the tree?
(arbitrary / ‘tree-implementation-detail’)
->ID-attribute must contain an XML name that is
unique within the document; more precisely: no other ID-attribute in the document may have the same value.

Name must start with a-zA-Z or with ‘_’ or with ‘:’ (also: no white space!)
Issue with the ID/IDREF solution:
-> On the EBAY-data, solution does not work (because of XML names)!
-> Would need to introduce additional IDs that are allowed ( one more level of indirection)

4. Entity Relationship Model
-> high-level database model
-> useful for design before moving to a lower level model 

ER Model has
→ Structural part 
- entity types
- attributes
- relationship types
→ Integrity constraints
- primary keys for entity and relationship types 
- multiplicity constraints for relationship types

ER Diagrams
→ relatively simple
→ user-friendly
→ unified view of data, independent of any implemented data mode.

Entity = a “thing” that exists and can be uniquely identified, e.g. an individual person
Entity type = collection of similar entities, e.g., a collection of people (rectangle)
Entity type has attributes (circles), representing properties of the entities.
Relationship Type = association between two or more entity types.(diamond)
Multiplicity Constraints in Relationship Types
→ Many-to-One (or One-to-Many)
An Employee Works in one Department or a Department has many Employees.
→ One-to-One
A Manager Heads one Department and vice versa.
→ Many-to-Many
A Lecturer Teaches many Students and a Student is Taught by many Lecturers

many to one
The arrowhead is drawn at the “one” end of rel. type
→ Each Emplyee Works-in one Department
→ Each Department has many Employees Working in it.
one to one
The arrowhead is drawn at both ends
→ Each Manager Occupies one Office
→ Each Office has one Manager Occupying it
many to many
No arrowheads
→ Each Lecturer Teaches many Students
→ Each Student is taught by many Lecturers

Participation constraints in relationships
→ optional (our default, sometimes indicated by multiplicity constraint 0..*)
e.g. Employee may or may not be assigned to a Department 

→ mandatory (double lines, or multiplicity constraint 1..*)

keys and superkeys

Superkey = Set of attributes of an entity type so that for each entity e of that type,
the set of values of the attributes uniquely identifies e. e.g. a Person may be uniquely identified by { Name, NI# }

Key = is a superkey which is minimal (aka “Candidate Key”)
e.g., a Person is uniquely identified by { NI# }.

Prime Attribute = attribute that appears in a key 
Non-Prime Attribute = attribute that appears in no key
Simple Key consists of one attribute
Composite Key consists of more than one attribute

Primary Key = a key that has been chosen as such by the database designer
→ primary key guarantees logical access to every entity (attributes of a primary key are underlined)

Weak Entity Type = an entity type that does not have sufficient attributes to form a primary key (double rectangle)
→ depends on the existence of an identifying (or “owner”) entity type (they have an “identifying (ID) relationship – double diamond)
→ must have a discriminator (dashed underline) for distinguishing its entities
E.g. in an employee database, Child entities exist only if their corresponding
Parent employee entity exists.

The primary key of a weak entity type is the combination of the primary key of its owner type and its discriminator.

ISA Relationship Types

If entities of a type have special properties not shared by all entities, then this suggests two entity types with an ISA relationship between them
→ AKA generalization / specialization (supertype / subtype rel.)
E.g. an Employee ISA Person and a Student ISA Person
→ If Employee ISA Person, then Employee inherits all attributes of Person.


Normal Forms
relational databases design

Bad database design causes problems, e.g. 
-> redundancy (facts are stored more than once)
-> inconsistency through update anomalies
-> complexity of queries and constrains

Normal Forms
→ First Normal Form (1NF)
→ Boyce-Codd Normal Form (BCNF) 
→ Fourth Normal Form (4NF)

Relationsl Model
-> attributes & domains: attribute A takes values from Dom(A)
-> relation schemas and database schemas 

Schema (or “table header”) of a relation (name) R
-> set schema(R) of attributes (or “column headers”) 

Database Schema
-> set of relation names together with their schemas

In relational algebra, duplicate rows are not permitted.
In SQL, they are permitted.
-> be careful about this
-> do not design tables that contain duplicates
(if you need them, administer them in a different way)
-> do not design queries that return duplicates
(unless that is really what you want! – often it is better to return a histogram)

We would like that
->the set of all attributes is a trivial superkey!
-> Then: every table has a PRIMARY KEY.

SQL queries have Multiset Semantics, i.e., answers contain duplicates.
Unless you use Set Operators (UNION, DIFFERENCE, INTERSECT, etc) (or the DISTINCT operator)
->duplicates are removed!

Normal Forms
-> prevent modification anomalies 
-> prevent data inconsistency
-> make tables less redundant
while preserving information (and dependencies)
Modification anomalies:
-> same information present in multiple rows. Partial updates may
result in inconsistent table (i.e., providing conflicting anwers) “update anomaly”
-> certain facts cannot be recorded at all “insertion anomaly”
-> deletion of data representing a fact may necessitate deletion of other completely different facts “deletion anomaly”

1NF = Choose Appropriate Data Types
2NF/3NF/BCNF= Do Not Represent the Same Fact Twice
4NF=Do not Store Unrelated Information in the Same Relation

Normalization = process of bringing a given database into a given normal form
Typically, normalization is achieved by decomposing tables into smaller tables.
Decomposition in turn is realized via projections.

1NF
-> for every attribute A, Dom(A) contains only atomic (indivisible) values
-> value of each attribute contains only a single value from the domain

A table is in 2NF, if
-> it is in 1NF
-> every non-prime attribute depends on the whole of every candidate key

Functional dependency D -> E: for every D-tuple, there is at most one E-tuple “E (functionally) depends on D”

Redundancy
Relation Schema R with functional dependency X → A
has fd-redundancy (with respect to X → A) if
(1) there exists a db instance D over R that satisfies X → A
(2) there exist two distinct` tuples in D that have equal (X, A)-values.

It should be clear to you that redundancy leads to update anomalies!

Third Normal Form (3NF)
A table is in 3NF, if
-> it is in 2NF
-> every non-prime attribute is non-transitively dependent on every candidate key

If X → A is nontrivial and A is non-key, then X must be a superkey!

Bring a 2NF table into 3NF:
-> move attribute involved in transitive dependency into a new table 
-> identify a primary key for the new table
-> make this primary key a foreign key of the original table

Foreign key = set of columns that references a set of columns of another table. 
The purpose of the foreign key is to ensure referential integrity:
only values appearing in the referenced table are permitted.

PRO: can always find decomposition preserving dependencies
CONTRA: some redundancy may remain
→ dependencies between prime attributes!

Boyce-Codd Normal Form (BCNF)
A table R is in BCNF, if for any dependency X -> Y at least one of the following holds
-> (X->Y) is trivial (i.e., Y is a subset of X) 
-> X is a superkey for R.

-> BCNF does not allow dependencies between prime attributes!
 BCNF = “3NF + no dependencies between (distinct) prime attributes”

3NF and BCNF are (potentially) not the same, if these conditions hold:
1) The table has two or more candidate keys
2) At least two of the candidate keys are composed of more than one attribute
3) The keys are not disjoint i.e. The composite candidate keys share some attributes

If R is a relation schema in BCNF then there are no fd-redundancies in R

BCNF 
Good: no FD-redundancy
Bad FDs may be lost

4NF
A table R is in 4NF, if for every multi-valued dependency (mvd) X -->> Y,
-> (X -->> Y) is trivial (i.e., Y is a subset of X, or, X union Y are all attributes)
-> X is a superkey for R

R has multi-valued dependency (mvd) X -->> Y
If two tuples agree on all attributes in X, then their Y-values
may be swapped, and the resulting two tuples must in R as well.


Bring a BCNF table into 4NF:
-> Move the two multi-valued sub-relations into separate tables 
-> Identify primary keys for each new table.

Relation Schema R with multi-valued dependency X -->> A
has mvd-redundancy (with respect to X -->> A) if
(1) there exists a db instance D over R that satisfies X -->> A
(2) there exist two distinct` tuples in D that have equal (X, A)-values.

If R is a relation schema in 4NF, then there are no mvd-redundancies in R

SQL

Despite the existence of the SQL standards, most SQL node is not completely protable among different database systems without adjustmets.

creating tables
create table <name> (attr1 type, attrN type);
Types
->char(n) fixed lenght string of exactly n characters
->varchar(n) variable length string of at most n characters
->int signed integer (4 bytes)
->smallint signed integer(2 bytes )
->float(M,D) / double (M,D) -floating point(4/8bytes)
M digits int total D digits after decimal point
->text/blob -text and binary strings(length <=2^16)
->date -date type MYSQL(yy-mm-dd) sqlite3(what ever format)
->time -time type MySQL(hh:mm:ss) sqlite3(what ever format)
->timestamp MYSQL (yy-mm-dd hh:mm:ss)

date/time/timestamp
-> can be compared for equality and less than

insertion
insert into t1 (select ..from .. where)

attributes of the result of the query must be same as those of T1.
→ MySQL is quite relaxed about this, it will often do the insertion.... 
→ sometimes unexpected behavior!

→ DELETE FROM T1; - delete all rows from table T1
→ DELETE FROM T1 where c3=1; - delete rows with c3-value equals 1
→ DROP TABLE T1; - remove table T1
→ ALTER TABLE T1 ADD COLUMN col1 int; - adds a column to table T1 
→ ALTER TABLE T1 DROP COLUMN col1; - removes a column from table T1

->describe t1; lists the fields and types of table t1(MySQL, not SQL)
(in sqlite3 this is done via “.schema t1” or “PRAGMA table_info(t1)”)
→ SHOW tables; - lists tables of your database (MySQL, not SQL!) 
(in sqlite3 this is done via “.tables”)

->default values fro some attributes:
-> create table t1 (<attribute><type>DEFAULT<value>)
→ ALTER TABLE Movies ADD COLUMN length int DEFAULT 0;

Constraints
→ PRIMARY KEY – primary means of accessing a table
→ NOT NULL – specifies that NULL is a forbidden value for the attribute
→ more than one key: UNIQUE

Inclusion Dependencies
→ inclusion dependency T1[a1,a2,...,aN] SUBSET T2[b1,b2,...,bN] means every (a1,...,aN)-projection of T1 is a (b1,...,bN)-projection of T2 “REFERENCES” keyword
→ often as part of a foreign key

CREATE TABLE Person (first_name char(20) NOT NULL,
                     last_name char(20) NOT NULL,
PRIMARY KEY (first_name,last_name));
CREATE TABLE Employee (first char(20) NOT NULL,
                       last char(20) NOT NULL,
FOREIGN KEY (first,last)
REFERENCES Person(first_name,last_name));

In relational algebra, duplicate rows are not permitted.
→ in SQL, the are permitted.
→ most queries have Multiset Semantics, i.e., answers contain duplicates.
→ not if you use set operators! E.g., UNION, INTERSECT, DIFFERENCE, etc
or the DISTINCT operator

>  SELECT DISTINCT col1 FROM T1;
> SELECT col1 FROM T1 UNION SELECT col2 FROM T1;

Set Operations with Duplicates
→ add “ALL” keyword
→ e.g. “UNION ALL” instead of “UNION”
>SELECT col1 FROM T1 UNION ALL SELECT col2 FROM T1;
-> “INTERSECT ALL” – keeps minimum (non-0) number of occ's of an element
→ MySQL does not support INTERSECT and INTERSECT ALL
-> “EXCEPTALL” – subtracts multiplicities

select xx from R,S,T xxxx ; where T is empty-->result is always empty
We select from the Cartesian product of R, S, and T!
→ empty if one of the tables is empty!

SQL Queries
 SELECT list, of, attributes --> optionally with aggregates
 FROM list of tables 
 WHERE conditions
 GROUP BY list of attributes
 ORDER BY attribute ASC | DESC

Aggregates: COUNT, SUM, AVG, MIN, MAX
Conditions: AND, OR, NOT, IN, <, =, >, LIKE
Combine tables (using set-semantics): UNION, INTERSECT, EXCEPT

-> query returns a table
-> where a table is allowed, you can place a nested query: (SELECT * FROM ... )

where xxx like 'xxx%' multiple characters including empty
where xxx like 'xxx_' one character

grouping wo aggregation
> SELECT col1,COUNT(col1) FROM T1 GROUP BY col1;

SELECT Z.a,min(Z.b) FROM (
SELECT R1.a,R1.b FROM R1 JOIN R2 ON R1.a=R2.a UNION ALL SELECT R2.a,R2.b FROM R1 JOIN R2 on R1.a=R2.a ) Z
GROUP BY Z.a;
Mysql often requires a name for nested queries 

MYSQL null is not allowed for a primary key attribute
sqlite3 null is allowed 

where 语句 cannot contain Aggregates
having aggregate(attribute) operator value

<value> <condition> ANY(<query>) is true if for some <value1> in the result of <query>,<value><condition><value1> is true
<value> <condition> ALL(<query>) is true if either:
-<query> evaluates to the empty set, or
-for every <value1> in the result of <query>,<value><condition><value1> is true

What is the most important (and expensive) SQL operation? → the JOIN

→ the simplest join is just the Cartesian product. 
→ its size is quadratic!
SELECT * FROM Numbers JOIN Numbers N2; = SELECT * FROM Numbers, Numbers N2;

Table1 JOIN Table2 USING (c1, c2, ..., cN)
→ joins all tuples of Table1 and Table2 which agree on
their c1,..,cN values
→ result table has columns c1,..,cN,
followed by the columns of Table1 that are not in { c1,..,cN } 
followed by the columns of Table2 that are not in { c1,..,cN }

T1 JOIN T2 ON (T1.c1=T2.d1 AND T1.c2<=T2.d2 OR NOT( ... ))
→ joins all tuples of Table1 and Table2 which satisfy join condition
→ result table has all columns of Table1 followed by all columns of Table2

outer join
Table1 RIGHT OUTER JOIN Table2 USING / ON ...
→ joins all tuples of Table1 with Table2 satisfying join condition,
plus all remaining tuples from Table2 (the RIGHT)
→ result tuples of the second type above have NULL-values in the columns coming from Table1.

Table1 LEFT OUTER JOIN Table2 USING / ON ...
→ joins all tuples of Table1 with Table2 satisfying join condition,
plus all remaining tuples from Table1 (the LEFT)
→ result tuples of the second type above have NULL-values in the columns coming from Table2.

NATURAL JOIN
natural left join
natural right join
natural full outer join

→ no full outer join in mysql

sort merge join

-> a B-tree index is nothing else but a sorted search-tree that behaves well on disk
-> even having such sorted B-tree indexes, efficient join processing remains a tremendous challenge

→ you would create B+tree indexes on longitude and latitude 
→ CREATE INDEX long on Item_coordinates(longitude);
→ CREATE INDEX lat on Item_coordinates(latitude);

MySQL
→ provides spatial indexes (an R-tree index, in particular) 
→ spatial index can be created for spatial attributes

Spatial Types
→ POINT
→ LINESTRING 
→ POLYGON 
→ GEOMETRY
→ MULITPOINT
→ MULTILINESTRING
→ MULTIPOLYGON
→ GEOMETRYCOLLECTION

POINT
-> 2-dimensional
-> X-coordinate and Y-coordinate
-> is a zero-dimensional GEOMETRY
CREATE TABLE Item_xy (item_id PRIMARY KEY, xy POINT);
INSERT INTO Item_xy VALUES (123456, POINT(-5.03434, 19.999));

->POINT has no display function
->either use X(.) and Y(.) to obtain X- and Y-values 
->or use AsText(.)
SELECT item_id,X(xy),Y(xy) FROM Item_xy;
or SELECT item_id,AsText(xy) FROM Item_xy;

LINESTRING
→ string of lines connecting a list of one ore more points
→ is a one-dimensional GEOMETRY
> SET @ls = GeomFromText('LineString(1 1,2 2,3 3)');
> SELECT NumPoints(@ls); -----3
> SELECT AsText(PointN(@ls,3)); ------POINT(3 3)
> SELECT GLength(@ls); 
> SELECT IsClosed(@ls); -------0

> SET @ls = GeomFromText('LineString(1 1,2 2,3 3 1 1)');
> SELECT IsClosed(@ls); ---------1

POLYGON
→ closed linestring, describes a planar surface 
→ is a two-dimensional GEOMETRY
Polygons of different kinds:
→ open (excluding its boundary)
→ bounding circuit only (ignoring its interior)
→ closed (both)
→ self-intersecting with varying densities of different regions.

> SET @poly = GeomFromText('Polygon(0 0,0 3,3 0,0 0)');
> SELECT Area(@poly);
+-------------+
| Area(@poly) |
+-------------+
| 4.5 | +-------------+
> SELECT AsText(Centroid(@poly));
+-------------------------+
| AsText(Centroid(@poly)) |
+-------------------------+
| POINT(1 1)              |
+-------------------------+

> SET @poly = GeomFromText('Polygon((0 0,0 3,3 0,0 0),
(1 1,1 2,2 1,1 1))');<--excluded>
> SELECT Area(@poly); 
+-------------+
| Area(@poly) | 
+-------------+ 
|4| 
+-------------+

> SET @poly = GeomFromText('MultiPolygon( ((0 0,0 3,3 0,0 0)), 
((1 1,1 2,2 1,1 1)) )');<--added>
> SELECT Area(@poly); 
+-------------+
| Area(@poly) | 
+-------------+ 
|5| 
+-------------+

> SELECT NumInteriorRings(@poly); 
+-------------------------+
| NumInteriorRings(@poly) | 
+-------------------------+ 
|1| 
+-------------------------+
> SELECT AsText(InteriorRingN(@poly,1)); 
+--------------------------------+
| AsText(InteriorRingN(@poly,1)) | 
+--------------------------------+
| LINESTRING(1 1,1 2,2 1,1 1) | 
+--------------------------------+
> SELECT AsText(ExteriorRing(@poly));
+-----------------------------+
| AsText(ExteriorRing(@poly)) |
+-----------------------------+
| LINESTRING(0 0,0 3,3 0,0 0) |
+-----------------------------+

POINT, LINESTRING, and POLYGON are subtypes of GEOMETRY
→ a GEOMETRYCOLLECTION gc contains any number of geometries, i.e., of points, linestrings, and polygons
→ NumGeometries(gc) – the number of geometries in collection gc 
→ GeometryN(gc, n) – the geometry number n

MySQL provides SPATIAL INDEXES (R-trees) for spatial types
→ but only for tables of certain types: 
– MyISAM Storage Engine
– InnoDB Storage Engine

CREATE TABLE Item_xy (item_id PRIMARY KEY, xy NOT NULL POINT)
ENGINE=MYISAM;
CREATE SPATIAL INDEX xy_index ON Item_xy (xy);
-> engine = MYISAM
-> all parts of a spatial index must be not null

→ MySQL lets you test geometric relationships, based on
Minimum Bounding Rectangles (aka Bounding Boxes or Envelops)
g1,g2: geometries (such as point, line, or polygon)
→ MBRContains(g1,g2) 
→ MBRCoveredBy(g1,g2) 
→ MBRCovers(g1,g2)
→ MBRDisjoint(g1,g2)
→ MBREqual(g1,g2)
→ MBRIntersects(g1,g2) 
→ MBROverlaps(g1,g2) 
→ MBRTouches(g1,g2) 
→ MBRWithin(g1,g2)

return((ACOS( SIN(x1*PI()/180)*SIN(x2*PI()/180)+
COS(x1*PI()/180)*COS(x2*PI()/180)*COS((y1-y2)*PI()/180)) *180/PI())*60*1.1515);

R-trees
→ R-Trees can organize any-dimensional data
→ data represented by minimum bounding boxes
→ each node bounds it’s children
→ a node can have many objects in it
→ the leaves point to the actual objects (stored on disk probably) 
→ the height is always log n (it is height balanced)

An entry E in a non-leaf node is defined as:
E = (I, child-pointer)
where the child-pointer points to the child of this node, and I is the MBR that encompasses all the regions in the child-node’s pointer’s entries.

Search Engine = tool to find documents from a collection that are good matches to a user query
Collections are, e.g., web pages, news articles, emails, etc.
Collections vary dramatically in size

Most text querying done
→ by content
→ satisfies an information need
A document matches an information need, if the user perceives it to be relevant.
→ relevance is inexact!
→ a document may be relevant, but contain none of the query terms
or irrelevant, even though it contains all the query terms.
A system is effective, if a good proportion of the first k search results are relevant.

→ bag-of-words queries
Parsing method for extracting terms from text:
→ should HTML markup be indexed?
→ or terms that appear within markup?
→ hyphenated words, considered as one or two words?

More fundamentally:
→ stemming? (= remove variant endings of a word)
→ casefolding? (= convert to lowercase)
→ stopping? (= remove common / functions words, e.g. “the”)
→ define similarity measure S( Q, D )
→ how to define a good similarity measure?
(1) give higher score if many query terms appear in the document (many times) 
(2) give less weight to terms that appear in many documents
(3) give more weight to terms that appear many times in a document
(4) give less weight to documents that contain many terms.

 Term Frequency (TF)
f(D,T) = how many times does term T appear in document D?
Document Frequence (DF)
f(T) = in how many documents of the collection does term T appear?
Inverse Document Frequence (IDF)
1 / f(T)
TF * IDF = f(D,T) / f(T)

IDF = ln (1 + N / DF) – “scaled” (n= number of documents in the collection)

→ angle between DOC-k and Q determines similarity
(length of vector not important)
→ “relative closeness” of term weights

Fast query evaluation makes use of an Index.
Index = datastructure that maps terms to documents containing them


3. Inverted Indexes / Files
Inverted File = for each distinct word T, contains
→ f(T) (#documents that contain T)
→ pointer to the corresponding inverted list

Inverted List of T = pairs < D, f(D,T) >
Listing each document D that contains T,
with number f(D,T) of occurrences of T in D
Thumb rule for effective retrieval:
→ index all terms, even stop words, numbers, etc.

w(d,t) = 1 + ln f(D,T)
query score S(q, d) 
→ inverted lists are stored contiguously
→ vocabulary stored in simple extensible structure (e.g., B-tree) (may be preprocessed by stemming and stopping)
→ inverted lists consist of doc numbers with #occurrences (possibly augmented by word positions)
→ ranking involves a set of accumulators and term-by-term processing of inverted lists

→ you can choose different Analyzers to do 
– casefolding
– stemming (wrt a given language) 
– stopping (wrt a given language)
→ you can insert documents into a collection and let Lucene generate inverted files for you (= “indexing” – very efficient!)

→ you can then (very efficiently) retrieve the k top-most relevant documents in your collection!
→ ranking function is a bit more sophisticated

Private static TopDocs search(String searchText); ...
IndexReader indexReader = DirectoryReader.open(directory);
IndexSearcher indexSearcher = new IndexSearcher(indexReader);
QueryParser queryParser = new QueryParser(searchField, new SimpleAnalyzer());
Query query = queryParser.parse(searchText);
TopDocs topDocs = indexSearcher.search(query,10000); System.out.println("Number of Hits: " + topDocs.totalHits); for (ScoreDoc scoreDoc:topDocs.scoreDocs) {
Document doc = indexSearcher.doc(scoreDoc.doc); System.out.println("doc_id: " + doc.get("doc_id")
   }
+ ", score: " + scoreDoc.score + " [" + doc.get("line") +"]");
 
SimpleAnalyzer → filters LetterTokenizer with LowerCaseFilter
LetterTokenizer
→ divides text at non-letters.
→ tokens as maximal strings of adjacent letters,
as defined by java.lang.Character.isLetter() predicate.
StandardAnalyzer -> filters StandardTokenizer with StandardFilter, LowerCaseFilter and StopFilter, using a list of English stop words.
--stopFilter filters and the in ...
EnglishAnalyzer(stemming) search keeping return keeps keep ...



Online Pattern Matching on Strings
Given – short string P (pattern) – long string T (text)
→ may preprocess P!

1) Automaton Method
→ build “match automaton A” for P and run A over T
2) Knuth-Morris-PrattAlgorithm
→ build jump-table for P and use it when traversing T
3) Boyer-Moore Algorithm
→ similar to KMP, but match backwards in P

naive method 
worst-case time compelxity
m:=|P|
N:=|T|
m(n-m+1)comparisions--take O(mn)time.

Word v is a suffix of word w, if w = uv for some u. (“proper suffix”, if u is non-empty)
Word u is a prefix of w, if w = uv for some v. (“proper prefix”, if v is non-empty)
(or: postfix)
Word u is a factor of w, if there are v and v’ such that w = vuv’

Automaton Method
→ Deterministic Finite Automaton
→ O(|P||S|) size, where S = alphabet
→ simply run it in O(|T|) time to determine all occurrences of P in T

→ for state k and symbol x, how to build transition d(k,x)?
→ length of the longest proper suffix of P[1] ... P[x]x that is prefix of P

→ matching time: O(n) n = |T| nice! m = |P|
→ preprocessing time: O(m * |S|) canbe O(m*m) not so nice

lospre(u, v) = length of longest
proper suffix of u that is prefix of v

MP[ k ] = lospre( P[1..k], P )

Morris-Pratt(1970) delay
Knuth-Morris-Pratt (KMP)

→ find longest lospre, such that next-letter != fail-letter
→ if does not exist, then mark “–1” = ADVANCE (and match with P[1]) = no further check (delay)
KMP[j] largest k >= 0 such that strong_cond(j,k) holds, or -1 if such k does not exist

strong_cond(j,k) : P[1...k] is a proper suffix of P[i..j] and P[k+1] !=P[j+1]
Matching complexity of KMP: O(m + n)
→ what is the maximum delay for KMP?
→ in O(log m) [Knuth]
→ can actually occur (e.g., for Fibonacci strings)

For KMP, delay(m) = O(loG m) and the bound is tight

Boyer-Moore
Match RIGHT-TO-LEFT in window
For each letter z, let
R(z) = distance from right-most occurrence of z in P, to the end of P
(and |P| if there is no occurrence)
→ shift R(a) to the right at mismatch with “a” (for all smaller shifts, we get a mismatch)

→ How does Google Chrome search text (Ctrl^ F) on a page so quickly? It uses a search algorithm inspired by Boyer-Moore and
Boyer-Moore-Horspool
→ V8 string search package (chromium project)


idea 2 

for every suffix u of P, let L(u) = lospre(u, P)
if mismatch after cu on symbol z, then
  k = max( R(z), D(u) )
  k = min( k, |P|-L(u) )
else
    report occurrence of P
    k := |P|-L(u)
shift by k

Horspool

For each letter z, let
R(z) = distance from right-most occurrence
of z in P[1..,m–1], to the end of P (and |P| if there is no occurrence)

Given
– a long string T (text)
– a short string P (pattern) m = |P|
Problem 1 find all occurrences of P in T 
Problem 2 count #occurrence of P in T
Offline Search = Indexed Search
= (linear time) preprocessing of T
Highlights → O(m) time for Problem 1
→ O(m + #occ) time for Problem 2
 Independent of size of text T!!!

naive solution
list all substrings of T, together with their occurrence lists
Lexicographically sort the substrings
Search occurrences of P:
→ jump to substrings starting with letter P[1] → from there, jump to substrings with
next letter P[2]
Etc.
after m jumps, reach (or not) matching substring
with its occurrence list
Search Time O(m)
Indexing time >O(n^2)

Suffix trie
→ O(m) count time
If we can count #black nodes of a
subtree in constant time.
→ O(m + #occ) retrieval time
If we can iterate through the leaves of a subtree with constant delay

No sorting, but
→ still quadratic in n, i.e., O(n2) :-( → the size (#nodes) of trie is O(n2)

new idea
->collapse paths of white nodes
→ add end marker “$”
→ one-to-one correspondence of
leaves to suffixes
→ a tree with n+1 leaves (and no nodes with only one child) has <= 2n+1 nodes!

Lemma
Size of suffix tree for “T$” is linear in n=|T|, i.e., in O(n).

→ search time still O(|P|), as for suffix trie! → perfect data structure for our task!

Suffix link

Definition

if x=ay is the string correspoding to a node u in the ST then the suffix link suf[u] is the node v corresponding to y in ST

using suffix links, we can online build the suffix-trie of T in time O(|suffix-Trie(T)|)



suffix array
given text T of length n for i = 1...n SA[k]= i if suffix T[i..n] is at position k in the lexicographic order T's suffixes 


Theorem
The suffix array of T can be constructed in time O(|T|).

Using binary search on SA(T), all occurrences of P in T can be located in O(|P|* log|T|)time.

→ O(|P| + log|T|) in practise, using a simple trick
→ O(|P| + log|T|) guaranteed, using LCP-array
LCP(k,j) = longest common prefix of T[SA[k]...] and T[SA[j]...]

Burrows-Wheeler Transfrom

generate all cyclic shifts of T
sort them lexicographically----$<a<b<c
first column: → sorted #occ of each letter:
second column: → “sorting with respect to considering one previous letter” = sorting of all two-letter substrings!

given only last column-->retrival the whole string

naive:
sort the last column --> first column 
last column is the previous column of first column 
then we got all 2-letter substring
sort 2 leeter substring
then add the last column in front of 2 letter substrings

Naive method: very expensive! (many sortings)
rankb( L, k ) = #occ of b in L, up to position k (excluding k)

C[]: first line starting with the letter in the first column
L[]: last column
Last-to-Front Mapping 
LF(k)=C[L[k]] + rankL[k]( L, k )

starting from $ (position k)
LF(k) = i put L(i) in front of $
LF(L(i)) = xx ...
and so on

What is special about the BWT?
→ efficient backward search!
→ counting #occ’s of pattern P in O(|P| log |S|) time!

Backward serch for PatternP[1]...P[m]

BWT Construction
→ use the suffix array SA(T)!
→ BWT[ k ] = T[ SA[ k ] – 1 ] (assuming T[0]=$)

XPath

low-level query language to select nodes of an XML document
most important XML query language: used in many technologies such as XQuery. XSLT, Xpointer, Xlink, Javascript,...

Terminology: instead of "query" we often say XPath expression
->an expression is the primary construction of the XPath grammar; it matches the production Expr of the XPath grammar.

XPath Data Model: 7 types of nodes
-> root nodes
-> element nodes
-> text nodes
-> attribute nodes
-> namespace nodes
-> processing instruction nodes
-> comment nodes

in abbreviated syntax
q1: /bib/book/year 
bib child nodes of root node 
q3: /a/b//d 
all d-nodes in the subtree of b
q4:/*/c 
q5://c
q6://*

important: there is always a (virtual) root-node!
/a = a-child of Root-node
/a/../* = same node
/a/../..//a = “No Match” 


/a is abbreviation for /child::a
//a is abbreviation for /descendant-or-self::node()/child::a
. is abbreviation for self::node()
.. is abbreviation for parent::node()

Predicates(aka "Filters")
q7: //c[./b] has b-child

Location Steps & Paths

A location Path is a sequence of Location Steps
A location Step is of the form
axis::nodestest[Filter_1][Filter_2]..[Filter_n]

Filters 
-> evaluate to true/false
->Xpath queries, evaluated with context-node = current node

nodetest: * or node-name(could be expanded->namespaces) or
-> text()
-> comment()
-> processing-instruction(ln)
->node()

child::text() select all text node children of the context node
-> the nodetest node() is true for any node
attribute::* select all attributes of the context node

following: Selects everything in the document after the closing tag of the current node
following-sibling: Selects all siblings after the current node

ancestor: Selects all ancestors (parent, grandparent, etc.) of the current node

preceding:Selects all nodes that appear before the current node in the document, except ancestors, attribute nodes and namespace nodes

//attribute::* ->all attributes
//attributes::a/.. gives 

//*[attributes::a=1] number comparison
//*[attributes::a="1"] string comparision
//*[attributes::a="1.0"] string comparision

attribute:: is abbreviated by @

useful function (Strings)

*/*[position()=1]/*[position()=2]/*[position()=2]
same as
*/*[1]/*[2]/*[2]


XPath Evaluation
can be done polynomial time
based on context-value tables
careful recording of unique values(no dupicates)

XSLT
Extensible Stylesheet Language Transformations
All major browsers(chrome, Firefox, IE, Safari, etc) support XSLT
->if an XML document has an XSL stylesheet associated with it, the browser will transform it on-the-fly

→ XML to HTML – for browser display
→ XML to LaTeX – for TeX layout
→ XML to SVG – graphs, charts, trees
→ XML to tab-delimited – for DB/stat packages
→ XML to plain text, e.g., PDF – for printing

XSLT vs. custom SAX/DOM traversal
 → smaller code
-> better readabillity & maintainability
->let XSLT compiler attempt to stream the transformation

stream 
->best effort approach
->very hard to detect statically
->XSLT 3.0

XSLT program
match = "para"
→ changes “para” nodes to “p”-nodes
→ deletes all other element nodes
→ keeps all text-nodes!

match = "node()"
→ all nodes are matched and taken over
→ except attributes nodes (they are deleted)

match="node() | @*"
→ all nodes are matched and taken over

