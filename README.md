# SQLI-on-Avaya-Experience-Portal
Researcher Attribution: Lui Man Ho, Rex and Chan Shing Hei, Stanley

Summary:
A critical vulnerability was identified in Avaya Experience Portal version 8.1.2.3 where an authenticated user can perform a SQL Injection against the underlying PostgreSQL database. This vulnerability can be further escalated to achieve Remote Code Execution (RCE) on the host operating system, allowing for complete system takeover.
 
Vulnerable Version and Product:
Avaya Experience Portal version 8.1.2.3
 
Vulnerability information and Proof of Concept:
 
Vulnerability Authenticated PostgreSQL Injection to RCE in Avaya experience platform. 
CVSS: 8.4 (High) 

It was found that the User role > Delete function is vulnerable to SQL injection. Any admin user can add a new user and inject SQL statement within Role’s name. While delete function is triggered on the selected role, it was observed that the Avaya Experience portal the name parameter will be injected into the SQL statement and can lead to authenticated Remote Code execution on the Avaya Experience Portal hosting server. The following screenshot showed the synopsis of the SQL injection while delete injected ROLE with value “gli1lpc1 `z’z”${{%{{\”. 
