# Normalization and Functional Dependencies

## 1. What is Normalization?

**Normalization** is the process of organizing data in a database to:

- Reduce data redundancy
- Avoid data anomalies
- Improve data consistency
- Organize data into well-structured tables
- Maintain relationships between data properly

The main normal forms commonly discussed in interviews are:

```text
1NF
↓
2NF
↓
3NF
↓
BCNF
```

---

# 2. Why Do We Need Normalization?

Consider this table:

```text
STUDENT_COURSE

student_id | student_name | course_id | course_name | instructor
-----------|--------------|-----------|-------------|-----------
101        | Ravi         | C01       | Python      | Kumar
101        | Ravi         | C02       | SQL         | Priya
102        | Arun         | C01       | Python      | Kumar
```

Here, student and course information is repeated.

For example:

```text
101 | Ravi
```

appears multiple times.

Similarly:

```text
C01 | Python | Kumar
```

is repeated.

This can cause problems when data is inserted, updated, or deleted.

Normalization helps reduce these problems.

---

# 3. What is Data Redundancy?

**Data redundancy** means unnecessary duplication of data.

Example:

```text
student_id | student_name | course
-----------|--------------|--------
101        | Ravi         | Python
101        | Ravi         | SQL
101        | Ravi         | Java
```

`Ravi` is repeated for every course.

Some repetition may be necessary depending on the database design, but unnecessary duplication is what normalization tries to reduce.

---

# 4. What are Data Anomalies?

Poorly designed tables can cause three major types of anomalies:

1. Insert anomaly
2. Update anomaly
3. Delete anomaly

These are very important interview topics.

---

# 5. What is an Insert Anomaly?

An **insert anomaly** occurs when we cannot insert certain information without unnecessarily adding unrelated information.

Example:

```text
STUDENT_COURSE

student_id | student_name | course_id | course_name
-----------|--------------|-----------|------------
101        | Ravi         | C01       | Python
```

Suppose a new course is created:

```text
C02 | SQL
```

but no student has enrolled yet.

If the table requires a student for every row, we may not be able to store the course information independently.

This is an insert anomaly.

---

# 6. What is an Update Anomaly?

An **update anomaly** occurs when the same information is stored in multiple rows and changing it requires updating multiple records.

Example:

```text
student_id | student_name | course_id | course_name | instructor
-----------|--------------|-----------|-------------|-----------
101        | Ravi         | C01       | Python      | Kumar
102        | Arun         | C01       | Python      | Kumar
103        | Priya        | C01       | Python      | Kumar
```

If the instructor changes from:

```text
Kumar → Raj
```

we need to update multiple rows.

If one row is missed:

```text
Kumar
Raj
Raj
```

the database becomes inconsistent.

---

# 7. What is a Delete Anomaly?

A **delete anomaly** occurs when deleting one piece of information unintentionally removes another important piece of information.

Example:

```text
student_id | student_name | course_id | course_name
-----------|--------------|-----------|------------
101        | Ravi         | C01       | Python
```

If Ravi drops the Python course and we delete this row, we may also lose the only information about the existence of the Python course.

This is a delete anomaly.

---

# 8. Three Main Anomalies

| Anomaly | Problem |
|---|---|
| Insert anomaly | Cannot insert data independently |
| Update anomaly | Same data must be updated in multiple rows |
| Delete anomaly | Deleting one fact unintentionally removes another fact |

### Memory Trick

```text
INSERT → Can't add
UPDATE → Must change multiple places
DELETE → Accidentally loses information
```

---

# 9. What is Functional Dependency?

A **functional dependency (FD)** describes a relationship where one attribute or set of attributes determines another attribute or set of attributes.

It is written as:

```text
A → B
```

and read as:

> A determines B.

---

# 10. Simple Functional Dependency Example

Consider:

```text
student_id | student_name
-----------|-------------
101        | Ravi
102        | Priya
103        | Arun
```

If each `student_id` identifies exactly one student name:

```text
student_id → student_name
```

This means:

> Given a student_id, we can determine the corresponding student_name.

---

# 11. What Does "Determines" Mean?

Suppose:

```text
student_id = 101
```

always corresponds to:

```text
Ravi
```

Then:

```text
student_id → student_name
```

If the same `student_id` were associated with both:

```text
Ravi
Arun
```

then the functional dependency would not hold under that data model.

---

# 12. Functional Dependency Example

Consider:

```text
employee_id | employee_name | department_id
------------|---------------|--------------
101         | Ravi          | D01
102         | Priya         | D02
103         | Arun          | D01
```

Functional dependencies can include:

```text
employee_id → employee_name
employee_id → department_id
```

because one employee ID identifies one employee and their department.

If each department has one department name:

```text
department_id → department_name
```

may also hold.

---

# 13. Determinant

In:

```text
A → B
```

`A` is called the **determinant**.

Example:

```text
student_id → student_name
```

Here:

```text
student_id = determinant
student_name = dependent attribute
```

---

# 14. Full Functional Dependency

A functional dependency is **fully dependent** when an attribute depends on the entire determinant and not on just a part of it.

This becomes especially important with composite keys.

Example:

```text
(student_id, course_id) → grade
```

Suppose the primary key is:

```text
(student_id, course_id)
```

and the grade depends on both the student and the course.

Then:

```text
(student_id, course_id) → grade
```

is a full functional dependency.

---

# 15. Partial Dependency

A **partial dependency** occurs when a non-key attribute depends on only part of a composite key rather than the whole composite key.

Example:

```text
ENROLLMENT

student_id | course_id | student_name | course_name | grade
-----------|-----------|--------------|-------------|------
101        | C01       | Ravi         | Python      | A
101        | C02       | Ravi         | SQL         | B
102        | C01       | Arun         | Python      | A
```

Suppose:

```text
Primary Key = (student_id, course_id)
```

But:

```text
student_id → student_name
```

and:

```text
course_id → course_name
```

Therefore:

```text
student_name
```

depends only on `student_id`.

And:

```text
course_name
```

depends only on `course_id`.

They do not depend on the complete composite key.

These are **partial dependencies**.

---

# 16. Transitive Dependency

A **transitive dependency** occurs when a non-key attribute depends on another non-key attribute through the key.

Example:

```text
employee_id → department_id
department_id → department_name
```

Therefore:

```text
employee_id → department_name
```

through:

```text
department_id
```

This is a transitive dependency.

### Simple Structure

```text
employee_id
     ↓
department_id
     ↓
department_name
```

Transitive dependencies are important when understanding **3NF**.

---

# 17. What is 1NF?

A table is in **First Normal Form (1NF)** when each column contains atomic values and there are no repeating groups or multi-valued attributes within a cell.

### Not in 1NF

```text
student_id | name | phone_numbers
-----------|------|----------------
101        | Ravi | 9876, 8765
```

The `phone_numbers` cell contains multiple values.

---

# 18. Converting to 1NF

Instead of:

```text
student_id | name | phone_numbers
-----------|------|----------------
101        | Ravi | 9876, 8765
```

we can use separate rows:

```text
student_id | name | phone
-----------|------|------
101        | Ravi | 9876
101        | Ravi | 8765
```

Each cell contains a single value.

---

# 19. 1NF Interview Definition

> A relation is in 1NF when its attributes contain atomic values and there are no repeating groups or non-atomic multi-valued fields.

### Remember

```text
1NF
↓
Atomic values
↓
No repeating groups
```

---

# 20. What is 2NF?

A table is in **Second Normal Form (2NF)** when:

1. It is already in 1NF.
2. No non-key attribute is partially dependent on a part of a composite candidate key.

### Important

**Partial dependency is the key concept for 2NF.**

---

# 21. 2NF Example

Consider:

```text
ENROLLMENT

student_id | course_id | student_name | course_name | grade
-----------|-----------|--------------|-------------|------
101        | C01       | Ravi         | Python      | A
101        | C02       | Ravi         | SQL         | B
102        | C01       | Arun         | Python      | A
```

Suppose:

```text
Primary Key = (student_id, course_id)
```

Dependencies:

```text
student_id → student_name
course_id → course_name
(student_id, course_id) → grade
```

The problem is:

```text
student_id → student_name
```

`student_name` depends only on part of the composite key.

Similarly:

```text
course_id → course_name
```

`course_name` depends only on part of the composite key.

Therefore, the table is not in 2NF.

---

# 22. Converting the Example to 2NF

Separate the data:

### Students

```text
student_id | student_name
-----------|-------------
101        | Ravi
102        | Arun
```

### Courses

```text
course_id | course_name
----------|------------
C01       | Python
C02       | SQL
```

### Enrollment

```text
student_id | course_id | grade
-----------|-----------|------
101        | C01       | A
101        | C02       | B
102        | C01       | A
```

Now:

```text
student_name
```

depends on:

```text
student_id
```

and:

```text
course_name
```

depends on:

```text
course_id
```

while:

```text
grade
```

depends on the complete key:

```text
(student_id, course_id)
```

---

# 23. Important Point About 2NF

A table with a **single-column candidate key** is automatically in 2NF if it is already in 1NF, because partial dependency requires a composite key.

This is a common interview question.

### Example

```text
employee_id → employee_name
```

If `employee_id` is a single-column key, there is no smaller part of the key to create a partial dependency.

---

# 24. What is 3NF?

A table is in **Third Normal Form (3NF)** when:

1. It is in 2NF.
2. It has no problematic transitive dependency of non-key attributes on a key.

A commonly used formal condition is:

> For every non-trivial functional dependency X → A, either X is a super key or A is a prime attribute.

For interview-level understanding, remember:

```text
3NF
↓
2NF
+
No transitive dependency of non-key attributes on a key
```

---

# 25. 3NF Example

Consider:

```text
EMPLOYEE

employee_id | employee_name | department_id | department_name
------------|---------------|---------------|----------------
101         | Ravi          | D01           | Engineering
102         | Priya         | D02           | HR
103         | Arun          | D01           | Engineering
```

Suppose:

```text
employee_id → department_id
department_id → department_name
```

Therefore:

```text
employee_id → department_name
```

through `department_id`.

This is a transitive dependency.

---

# 26. Converting the Example to 3NF

Split the table.

### Employee

```text
employee_id | employee_name | department_id
------------|---------------|--------------
101         | Ravi          | D01
102         | Priya         | D02
103         | Arun          | D01
```

### Department

```text
department_id | department_name
--------------|----------------
D01           | Engineering
D02           | HR
```

Now:

```text
employee_id → department_id
```

and:

```text
department_id → department_name
```

are stored in appropriate relations.

---

# 27. What is BCNF?

**BCNF (Boyce-Codd Normal Form)** is a stronger version of 3NF.

A relation is in BCNF if:

> For every non-trivial functional dependency X → Y, X is a super key.

### Simple Rule

```text
BCNF
↓
Every determinant must be a super key
```

---

# 28. 3NF vs BCNF

The main difference is:

```text
3NF
→ Allows a dependency X → A when A is a prime attribute,
  even if X is not a super key.

BCNF
→ Requires X to be a super key for every non-trivial FD.
```

Therefore:

```text
BCNF is stricter than 3NF.
```

A relation in BCNF is always in 3NF, but a relation in 3NF is not necessarily in BCNF.

---

# 29. BCNF Example

Consider a relation:

```text
R(Student, Course, Instructor)
```

Suppose the functional dependencies are:

```text
(Student, Course) → Instructor

Instructor → Course
```

If `Instructor` is not a super key, then:

```text
Instructor → Course
```

violates BCNF.

Why?

Because BCNF requires the determinant:

```text
Instructor
```

to be a super key.

If it is not, the relation is not in BCNF.

---

# 30. Normal Forms Summary

| Normal Form | Main Requirement |
|---|---|
| 1NF | Atomic values, no repeating groups |
| 2NF | 1NF + no partial dependency |
| 3NF | 2NF + no problematic transitive dependency |
| BCNF | Every determinant is a super key |

### Easy Memory Trick

```text
1NF → Atomic
2NF → No Partial Dependency
3NF → No Transitive Dependency
BCNF → Determinant must be Super Key
```

---

# 31. Normalization Example from Start to Finish

Suppose we have:

```text
STUDENT_COURSE

student_id | student_name | course_id | course_name | instructor | grade
-----------|--------------|-----------|-------------|------------|------
101        | Ravi         | C01       | Python      | Kumar      | A
101        | Ravi         | C02       | SQL         | Priya      | B
102        | Arun         | C01       | Python      | Kumar      | A
```

Assume:

```text
(student_id, course_id)
```

is the composite key.

Dependencies:

```text
student_id → student_name

course_id → course_name
course_id → instructor

(student_id, course_id) → grade
```

---

## Step 1: 1NF

Make sure every attribute contains atomic values.

Our values are atomic, so the table can satisfy 1NF.

---

## Step 2: 2NF

We identify partial dependencies:

```text
student_id → student_name

course_id → course_name
course_id → instructor
```

These depend only on parts of:

```text
(student_id, course_id)
```

So we separate them.

### Students

```text
student_id | student_name
-----------|-------------
101        | Ravi
102        | Arun
```

### Courses

```text
course_id | course_name | instructor
----------|-------------|-----------
C01       | Python      | Kumar
C02       | SQL         | Priya
```

### Enrollment

```text
student_id | course_id | grade
-----------|-----------|------
101        | C01       | A
101        | C02       | B
102        | C01       | A
```

Now the partial dependencies are removed.

---

# 32. Why Does Normalization Reduce Redundancy?

Before normalization:

```text
101 | Ravi | C01 | Python | Kumar
101 | Ravi | C02 | SQL    | Priya
102 | Arun | C01 | Python | Kumar
```

Information about:

```text
Ravi
Python
Kumar
```

can appear repeatedly.

After normalization:

```text
STUDENTS
101 | Ravi
102 | Arun

COURSES
C01 | Python | Kumar
C02 | SQL    | Priya

ENROLLMENT
101 | C01 | A
101 | C02 | B
102 | C01 | A
```

Each fact is stored in a more appropriate place.

---

# 33. What is Denormalization?

**Denormalization** is the intentional introduction of some redundancy into a database to improve read performance or simplify certain queries.

Normalization focuses on reducing redundancy.

Denormalization may intentionally add redundancy when performance or application requirements justify it.

### Example

Instead of joining:

```text
Orders
Customers
```

for every read, some systems may store selected customer information directly in an order-related table.

This can reduce joins but creates additional consistency/update considerations.

---

# 34. Normalization vs Denormalization

| Normalization | Denormalization |
|---|---|
| Reduces redundancy | Intentionally introduces some redundancy |
| Reduces anomalies | May increase update complexity |
| Improves logical organization | Can improve read performance |
| Uses more separated tables | May combine or duplicate data |
| Common in transactional design | Sometimes used for performance/reporting |

### Interview Answer

> Normalization organizes data to reduce redundancy and anomalies, while denormalization intentionally introduces some redundancy when it provides performance or practical benefits.

---

# 35. Functional Dependency vs Multivalued Dependency

A **functional dependency**:

```text
A → B
```

means one value of A determines one value of B under the relation's business rules.

A **multivalued dependency** is a more advanced concept used in higher normal forms such as 4NF.

For your core interview preparation, focus mainly on functional dependencies, partial dependencies, and transitive dependencies.

---

# 36. Why is 2NF Mainly Relevant to Composite Keys?

Partial dependency means:

```text
Part of a key → Non-key attribute
```

Therefore, a partial dependency requires a key with multiple attributes.

Example:

```text
(student_id, course_id) → grade
```

A dependency such as:

```text
student_id → student_name
```

can be partial because `student_id` is only part of the composite key.

With a single-column key:

```text
student_id
```

there is no smaller part of the key.

Therefore, a relation in 1NF with a single-column candidate key is automatically in 2NF.

---

# 37. How to Identify the Normal Form of a Table

Use this process:

```text
Step 1
↓
Are all values atomic?
↓
No → Not 1NF
Yes
↓
Step 2
↓
Is there a composite candidate key?
↓
If yes, check partial dependencies
↓
Partial dependency exists?
↓
Not 2NF
↓
Step 3
↓
Check transitive dependencies
↓
Transitive dependency exists?
↓
Not 3NF
↓
Step 4
↓
Check every determinant
↓
Every determinant is a super key?
↓
BCNF
```

---

# 38. Frequently Asked Interview Questions

## Q1. What is normalization?

### Answer

> Normalization is the process of organizing data into well-structured relations to reduce unnecessary redundancy and prevent insert, update, and delete anomalies.

---

## Q2. Why do we use normalization?

### Answer

> We use normalization to reduce data redundancy, avoid data anomalies, improve consistency, and organize data efficiently.

---

## Q3. What are the different normal forms?

### Answer

The commonly discussed normal forms are:

```text
1NF
2NF
3NF
BCNF
```

Higher normal forms such as 4NF and 5NF also exist, but 1NF through BCNF are the most important for many entry-level interviews.

---

## Q4. What is 1NF?

### Answer

> A table is in 1NF when its attributes contain atomic values and there are no repeating groups or multi-valued fields within a cell.

---

## Q5. What is 2NF?

### Answer

> A table is in 2NF when it is in 1NF and no non-key attribute is partially dependent on a part of a composite candidate key.

---

## Q6. What is 3NF?

### Answer

> A table is in 3NF when it is in 2NF and has no problematic transitive dependency of non-key attributes on a key. Formally, for every non-trivial FD X → A, X must be a super key or A must be a prime attribute.

---

## Q7. What is BCNF?

### Answer

> A relation is in BCNF if, for every non-trivial functional dependency X → Y, X is a super key.

---

## Q8. What is a functional dependency?

### Answer

> A functional dependency describes a relationship where one attribute or set of attributes determines another attribute or set of attributes.

Example:

```text
student_id → student_name
```

---

## Q9. What is a partial dependency?

### Answer

> A partial dependency occurs when a non-key attribute depends on only part of a composite candidate key.

---

## Q10. What is a transitive dependency?

### Answer

> A transitive dependency occurs when a non-key attribute depends on another non-key attribute through a key.

Example:

```text
employee_id → department_id
department_id → department_name

Therefore:

employee_id → department_name
```

---

## Q11. What are insertion, update, and deletion anomalies?

### Answer

> Insert anomaly occurs when data cannot be inserted independently. Update anomaly occurs when the same fact must be updated in multiple rows. Delete anomaly occurs when deleting one fact unintentionally removes another fact.

---

## Q12. What is data redundancy?

### Answer

> Data redundancy is unnecessary duplication of data in a database.

---

## Q13. What is denormalization?

### Answer

> Denormalization is the intentional introduction of some redundancy to improve read performance or simplify certain queries.

---

## Q14. What is the difference between 2NF and 3NF?

### Answer

> 2NF eliminates partial dependencies, while 3NF additionally eliminates problematic transitive dependencies.

```text
2NF → No Partial Dependency

3NF → No Transitive Dependency
```

---

## Q15. What is the difference between 3NF and BCNF?

### Answer

> BCNF is stricter than 3NF. In BCNF, every determinant of a non-trivial functional dependency must be a super key. 3NF allows a dependency where the determinant is not a super key if the dependent attribute is a prime attribute.

---

## Q16. Can a table be in 3NF but not BCNF?

### Answer

> Yes. BCNF is stricter than 3NF, so a relation can satisfy 3NF while still violating BCNF.

---

## Q17. Can a table be in 2NF but not 3NF?

### Answer

> Yes. A table can have no partial dependencies and still contain a transitive dependency.

---

## Q18. Can a table be in 1NF but not 2NF?

### Answer

> Yes. If it has a composite candidate key and a non-key attribute depends only on part of that key, it is in 1NF but not 2NF.

---

## Q19. Can a table with a single-column primary key violate 2NF?

### Answer

> A table in 1NF with only a single-column candidate key is automatically in 2NF because partial dependency requires a composite key.

---

## Q20. Does normalization always improve performance?

### Answer

> Not necessarily. Normalization improves structure and reduces redundancy, but highly normalized designs can require more joins. In some cases, controlled denormalization can improve read performance.

---

# 39. Scenario-Based Interview Questions

## Scenario 1

You have:

```text
student_id
course_id
student_name
course_name
grade
```

and the primary key is:

```text
(student_id, course_id)
```

Suppose:

```text
student_id → student_name
course_id → course_name
```

### Question

What problem exists?

### Answer

There are partial dependencies because `student_name` depends only on `student_id` and `course_name` depends only on `course_id`.

Therefore, the table violates 2NF.

---

## Scenario 2

You have:

```text
employee_id
employee_name
department_id
department_name
```

with:

```text
employee_id → department_id
department_id → department_name
```

### Question

What type of dependency exists?

### Answer

A transitive dependency exists:

```text
employee_id
     ↓
department_id
     ↓
department_name
```

This is a 3NF issue.

---

## Scenario 3

A table contains:

```text
101 | Ravi | 9876, 8765
```

### Question

Which normal form is violated?

### Answer

The table violates 1NF because one cell contains multiple phone values instead of an atomic value.

---

## Scenario 4

A course instructor's name is repeated across hundreds of rows. When the instructor changes, all rows must be updated.

### Question

What anomaly is this?

### Answer

**Update anomaly.**

---

## Scenario 5

A course cannot be added to the database until at least one student enrolls in it.

### Question

What anomaly is this?

### Answer

**Insert anomaly.**

---

## Scenario 6

Deleting the last student enrolled in a course also deletes the only record containing the course information.

### Question

What anomaly is this?

### Answer

**Delete anomaly.**

---

# 40. Interview-Friendly Normalization Example

If the interviewer asks:

> "Explain normalization with an example."

You can answer:

> Suppose we have a student-course table containing student details, course details, and enrollment details in the same table. This can cause redundancy and insert, update, and delete anomalies. We can normalize the table by separating Student, Course, and Enrollment information. 1NF ensures atomic values, 2NF removes partial dependencies caused by composite keys, and 3NF removes transitive dependencies. This results in a cleaner and more consistent database design.

---

# 41. Quick Revision Table

| Concept | Remember |
|---|---|
| Normalization | Organizes data and reduces redundancy |
| Redundancy | Unnecessary duplicate data |
| Insert anomaly | Difficulty adding independent data |
| Update anomaly | Same fact must be updated multiple times |
| Delete anomaly | Deleting one fact removes another |
| Functional dependency | A → B |
| Determinant | Left side of FD |
| Partial dependency | Depends on part of composite key |
| Transitive dependency | Key → non-key → non-key |
| 1NF | Atomic values |
| 2NF | 1NF + no partial dependency |
| 3NF | 2NF + no problematic transitive dependency |
| BCNF | Every determinant is a super key |
| Denormalization | Controlled redundancy for practical/performance reasons |

---

# 42. Final Memory Sheet

```text
NORMALIZATION
─────────────
Goal:
→ Reduce redundancy
→ Avoid anomalies
→ Improve consistency
→ Organize data


ANOMALIES
─────────
Insert
→ Cannot add independent information

Update
→ Same information must be changed in multiple rows

Delete
→ Deleting one fact accidentally removes another


FUNCTIONAL DEPENDENCY
─────────────────────
A → B

A = Determines B


PARTIAL DEPENDENCY
──────────────────
Part of composite key → Non-key attribute

Main issue:
→ 2NF


TRANSITIVE DEPENDENCY
─────────────────────
Key → Non-key → Non-key

Main issue:
→ 3NF


NORMAL FORMS
────────────
1NF
→ Atomic values
→ No repeating groups

2NF
→ 1NF
→ No partial dependency

3NF
→ 2NF
→ No problematic transitive dependency

BCNF
→ Every determinant is a super key


DENORMALIZATION
───────────────
Intentional redundancy
→ Can improve read performance
→ Can increase update/consistency complexity
```

# 43. Most Important Questions to Prepare

If you have limited time before an interview, prioritize these:

```text
1. What is normalization and why is it needed?
2. What are insert, update, and delete anomalies?
3. What is functional dependency?
4. What is a determinant?
5. What is partial dependency?
6. What is transitive dependency?
7. What is 1NF?
8. What is 2NF?
9. What is 3NF?
10. What is BCNF?
11. Difference between 1NF, 2NF, and 3NF
12. Difference between 3NF and BCNF
13. Can a table be in 3NF but not BCNF?
14. Why does 2NF mainly matter for composite keys?
15. Can a single-column key have partial dependency?
16. What are the benefits of normalization?
17. What is denormalization?
18. Normalization vs denormalization
19. Given a table and dependencies, identify its normal form
20. Given a poorly designed table, normalize it
```

# 44. Key Interview Takeaway

The most important chain to remember is:

```text
Normalization
      ↓
Reduce Redundancy
      ↓
Avoid Anomalies
      ↓
Use Functional Dependencies
      ↓
1NF → Atomic Values
      ↓
2NF → Remove Partial Dependencies
      ↓
3NF → Remove Transitive Dependencies
      ↓
BCNF → Every Determinant is a Super Key
```

If you understand this chain and can solve a small normalization example on a whiteboard, you are well prepared for the normalization portion of a typical DBMS interview.