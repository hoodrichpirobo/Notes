2025-09-13 14:43

Status: #adult #lectures

Tags: [[RA Operators]] [[Data Model]] [[BDA]] [[RDBMS]]

# BDA 1.2. The Relational Data Model

Most database management systems are relational.
Rows and tuples mean the same thing.
I'm thinking that what the teacher is trying to say is that there might be columns in a database  that relate different tables between them.
The order has no meaning but for simplicity we insert rows at then end with `INSERT`.
we delete using `DELETE`.
we also can modify thru `UPDATE`.
We will use SQL to express queries for the DBMS to understand and process automatically, we could also do it through relational algebra, relational calculus.

## RA Operators.
	$A\cup B$
	$A \cap B$
	$A \setminus B$
	We also have **projections**, which extracts the desired attributes (columns) of a table: $R[B,C]$
	We also have **selections**, which selects the tuples that satisfy the predicate: `WHERE [PRED]`
	Predicate is something like a condition.
	$A \bowtie B$
	
	  Write expressions to obtain: 
		1. Name  of all the subjects: 
			Subject[name]
		2. Name  of the subjects with 4 lab groups (LG): 
			(Subject WHERE LG = 4) [name]
		3. Name  of lecturers with category ‘Titular’ teaching the subject 11545 
 I should redo all of this myself later on. 
			(($Lecture \bowtie coedlec^{Teaching}$)WHERE category=Titular AND cod_sub='11545')$[name]$
		4. Name  of the lecturers with category “Titular” teaching a subject in the ‘1A’ semester.
			This is probable to be asked on exams
			
		5. Name of lecturers teaching a subject with 2 TG groups 
			
		6. Name  of lecturers with category=‘Titular’ and with no telephone number
			

There's homework on BDA, Exercise 1.2 from the slides.
	<details><summary>Spoiler Alert: </summary>
	No lo hice</details>

## Terminology
| Common terminology | RDM       |
| ------------------ | --------- |
| table              | relation  |
| row / record       | tuple     |
| column / field     | attribute |
| data type          | domain    |

**Example of tuple schema:**

Person = {(person_id, integer), (name, char), (address, char)}

where:

- { person_id, name, address } is the set of attribute names in the schema.  
- *integer, char, char* are the domains which are associated with the attributes.

## Tuple and relation

* **Relation schema** → the *structure* (attributes + domains). Example:
  `Person(person_id: integer, name: char, address: char)`

* **Relation** → the *data* (set of tuples) that follows the schema. Example:
  `{ (1, "Alice", "Spain"), (2, "Bob", "France") }`

Schema = design, Relation = content.

## Null value: AND, OR, NOT
| G         | H         | G ∧ H     | G ∨ H     |
| --------- | --------- | --------- | --------- |
| false     | false     | false     | false     |
| false     | true      | false     | true      |
| true      | false     | false     | true      |
| true      | true      | true      | true      |
| undefined | undefined | undefined | undefined |
| undefined | false     | false     | undefined |
| undefined | true      | undefined | true      |
| false     | undefined | false     | undefined |
| true      | undefined | undefined | true      |

| G         | ¬G        |
| --------- | --------- |
| false     | true      |
| undefined | undefined |
| true      | false     |

If you have some null values on your SQL queries you'll get unexpected results

## Primary Key and Relation

* **R** = the relation (e.g., `R = Person{person_id, name, address}`).
* **PK** = the *primary key* of R (a subset of attributes/column).
* Example:

  * `PK = {person_id}` → uniquely identifies each person.
  * Could also be `{name}` or `{address}` **if** those attributes are unique for all tuples.

So: **PK is just the chosen unique identifier for R (like Person).**


## References
[[BDA Concepts.]]