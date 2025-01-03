# Database security
Why? Databases are a critical point in data storage because they contain lots of data in a single point of access.
Database managements systems are complex systems with a language called SQL used to access the data.
## Relational databases
- Tables
  Relation in the form of a $N \times M$ matrix
- Field
  Column of the table
- Record
  Row of the table
- Primary key
  One or more fields that uniquely identify a row.
- Foreign key
  A primary key of another table that appears as a field of another table.
- View:
  Virtual table with selected rows and columns from one or more tables. Are used to hide data for security reasons
# Attacks on databases
## SQL Injection
The attacker triggers unexpected behaviour by supplying untrusted, malicious SQL query input to an application.
### Injection possible locations
#### User input
Input from forms is used to compose SQL queries
#### Server variables 
headers that are logged and might be modified by the attacker. For example, headers
logged for usage statistics.
#### Second-order injections
the attacker injects data in the database that is, in turn, used to compose another query
#### Cookies
Browser cookies are used to implement stateful sessions, but can be manipulated by the attacker. This can trigger injections when cookie value is used to compose queries.
#### Physical user input
input that comes from physical devices or media.
Examples are barcodes, RFID tags, scanned paper documents, $\dots$
## Types of attack
### Inband
Same channel for attack and communication of attack data result.
#### Tautology attack
This form of attack injects code in conditional statements so they always evaluate to true.
As a first example, this query tries to dump all data from a select statement:
```sql
' OR 1=1 --
```
Another type of attack:
End-of-line comment: legitimate code that follows is nullified through usage of end of line comments
```sql
--
```
Third type of attack:
Piggybacked queries: 
The attacker adds additional queries beyond the intended query, piggybacking the attack on top of a legitimate request
```sql
; DROP TABLE ...
```
### Inferential
The attacker leaks information not directly, he observes the result of the attack.
#### Incorrect SQL injection
The default error page returned by application servers is often overly descriptive, revealing sensitive information.
#### Blind SQL injection
An attacker infers the data present in a database even when the application does not display errors or data.
# Countermeasures
- Whitelisting input
- Strict typing on input
- Prepared statements
- Typed API
- Trusted input
- Sanitization as last resort
## Database Access Control
Controls access to features of the database.
### Priviledges
- GRANT
	- WITH GRANT OPTION means that a user that obtains these kind of privileges can also grant them to other users.
- REVOKE
	- CASCADE is used to revoke all permissions  from users that obtained permission through the revoked user.
