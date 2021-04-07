# Normalization
## Definition
It is a process of organizing a database into tables and columns, so the database becomes about specific topic and only supporting topics included.

## Reasons for normalization
* Remove duplicate data.
* Eliminate issues coming from database modifications.
* simplify queries.

## Data duplication and Modification Anomalies
when the table serves more that one purpose will make some issues including:
* Data Duplication, which will:
    * increase the storage and decrease performance.
    * become more difficult to maintain data changes.
* Modification anomalies, which are three types:
    1. Insert Anomaly, we can't record until we know information for the entire row.
    2. Update Anomaly, when a number changes, there will be multiple updates the need to be made.
    3. Deletion Anomaly,Deletion of row causes removal of more than one set of facts.
* Search and Sort Issues.
## Forms of normalization
To solve the previous issues, we have three forms of normalization, they are progressive which means we cannot get to the third form before finishing from the the first the the second.
* First Normal Form **(1NF)**:
    1. It should only have single(atomic) valued attributes/columns.
    2. Values stored in a column should be of the same domain
    3. All the columns in a table should have unique names.
    4. And the order in which data is stored, does not matter.
* Second Normal Form **(2NF)**:
    1. It should be in the first normal form.
    2. It should have partial dependency.
* Third Normal Form **(3NF)**:
    1. It should be in the second normal form.
    2. It doesn't have transitive dependency.
