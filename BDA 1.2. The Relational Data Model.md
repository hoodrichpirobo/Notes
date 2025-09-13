2025-09-13 14:43

Status: #child #lectures

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

## References
[[BDA Concepts.]]