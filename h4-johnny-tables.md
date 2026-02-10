# H4: Johnny Tables

---

## A01 - Broken Access Control
This happens when users can perform actions they should not be allowed to do, such as viewing or modifying someone else's information.

### Typical Issues
- Manually changing URLs or request data to access another user's account  
- Gaining admin-level abilities without proper authorization  
- APIs that do not enforce access checks correctly  
- Incorrect configurations, like insecure CORS rules or poorly set cookies  

### Why It Matters
Weak access control can expose private data, allow unauthorized operations, or even lead to a complete system takeover.

### Prevention Strategies
- Block access by default unless it is explicitly permitted  
- Centralize and reuse access control logic throughout the application  
- Record and monitor failed access attempts  

### Thoughts
It is surprising how something as simple as tweaking a URL can reveal sensitive information if access controls are not solid.

---

## A05 - Security Misconfiguration
This refers to systems or applications that are not set up securely, often leaving weak settings or default credentials in place.

### Common Examples
- Default accounts or sample applications left running on production servers  
- Error messages that reveal too much detail to users  
- Running outdated software or skipping security patches  

### Why It Matters
Attackers actively look for these weaknesses because they are easy entry points for stealing data or taking over systems.

### How to Prevent It
- Use a consistent, secure configuration process across all environments  
- Remove anything unnecessary from the system  
- Keep configurations, permissions, and software versions updated and reviewed regularly  
- Automate security checks and apply security headers  

### Thoughts
It makes you wonder whether these issues come from lack of knowledge or simply the pressure to release quickly.

---

## A06 - Vulnerable and Outdated Components
In simple terms, this happens when an application relies on old or insecure components that attackers can exploit.

### Risks Increase When
- You do not track which versions of components you are using  
- Updates and patches are not applied regularly  
- You rely on components that are no longer supported  

### Prevention
- Keep an inventory of all components and their versions  
- Remove anything that is not needed  
- Use tools that scan for known vulnerabilities  
- Download components only from trusted sources  

### Thoughts
Modern apps depend heavily on third-party libraries, and forgetting to update even one of them can create a major security hole. It definitely makes those update prompts feel more important.

---

## A03 - Injection
Injection attacks occur when attackers insert malicious input that tricks the system into executing unintended commands.

### Common Types
- SQL injection  
- OS command injection  
- NoSQL injection  
- ORM-related injection flaws  

### Prevention Methods
- Use parameterized queries or safe APIs  
- Validate and sanitize all user input  
- Avoid building queries by concatenating strings with user-supplied data  

### Thoughts
These vulnerabilities really show why data and executable code must always be kept separate.

---

## Munroe - xkcd 327: "Exploits of a Mom"
The comic features a mother who names her child `Robert'); DROP TABLE Students;--`, which is actually a malicious SQL command designed to delete a database table.

The teacher explains that the student's name caused the system to lose data - essentially an injection attack.  
The mother responds by saying they should have sanitized their inputs, highlighting the importance of validating user data to prevent such attacks.

---

## References
- Munroe, R. (n.d.). *Exploits of a Mom*. xkcd. https://xkcd.com/327/
- OWASP (2021). *A01:2021 - Broken Access Control*. https://owasp.org/Top10/A01_2021-Broken_Access_Control/
- OWASP (2021). *A05 Security Misconfiguration - OWASP Top 10:2021*. https://owasp.org/Top10/A05_2021-Security_Misconfiguration/
- OWASP (2021). *A06 Vulnerable and Outdated Components - OWASP Top 10:2021*. https://owasp.org/Top10/A06_2021-Vulnerable_and_Outdated_Components/
- OWASP (2021). *A03 Injection - OWASP Top 10:2021*. https://owasp.org/Top10/A03_2021-Injection/

---
# a) Goat - Install WebGoat 2023.4
---

## Installation
Using my virtual machine, I was able to install WebGoat 2023.4 successfully by following the guide provided by the teacher (Terokarvinen.com, 2023).

The same commands from the guide were used, which made the whole process smooth.

After installation, then for launching WebGoat I use the exact commands mentioned in the guide.  
The screenshot below (taken from the linux terminal) indicates a successful launch:

**<img width="339" height="72" alt="h4-Taska1" src="https://github.com/user-attachments/assets/2d98284c-546a-4d38-aac3-dacf961777bc" />**

## Accessing WebGoat
I changed the port as instructed in the guide and successfully open the URL in my browser, as shown below:

**<img width="264" height="190" alt="h4-Task-a2" src="https://github.com/user-attachments/assets/82eb4436-abcf-48c4-9559-c107a75866cc" />**

## Reference
Terokarvinen.com. (2023). *Try Web Hacking on New Webgoat 2023.4.*  
Available at: https://terokarvinen.com/2023/webgoat-2023-4-ethical-web-hacking/

---

# b) F12 - WebGoat 2023.4: General: Developer Tools

This challenge was included at the end of the Developer Tools lesson.

## Process

Initially, I studied and reviewed the chapters in the lesson to understand the content.
For the task, I opened the browser's Developer Tools by pressing **F12** on my keyboard.
Then I navigated to the **Network** tab and clicked the **"Go!"** button as instructed.
This generated a **POST** request, which contained more detailed information as also shown in the screenshot.
It took alot of time to find the number from the default **Headers** tab, but later I realized it might be under a different section.
Finally, I figured out that the **networkNum** value was located in the **Request** tab, where it could be accessed easily.

**<img width="640" height="285" alt="h4-Task-b" src="https://github.com/user-attachments/assets/11531088-b64c-46fc-8304-997654f0bff9" />**

## Learnings
This task demonstrated that important data such as `networkNum`- is often stored in the **Request payload** rather than in the headers or any other tab.  
It highlighted the need to examine every section of the Developer Tools, not just the default tabs, when performing security assessments.

---

# c) Update OS & Applications
I updated all operating systems by running the following commands:

```bash
sudo apt update
sudo apt full-upgrade -y
sudo reboot
```

## Reference
Bill Sky - The Computer Guy! (2024). Linux 04: How to update and install applications on Linux.  
YouTube. Available at: https://www.youtube.com/watch?v=GmqhbsaGk3I
Accessed 14 Sep. 2025.

---

# d) Sequel - SQLZoo Tasks

## 0. SELECT Basics
- I used the **WHERE** clause with a string match to retrieve the population of Germany, reinforcing how single quotes denote string values in SQL.  
- I employed the **IN** operator to filter results for multiple countries, learning how to efficiently check against a list of values.  
- I utilized the **BETWEEN** operator to find countries with areas within a specified range, gaining a clearer understanding of inclusive range checks in SQL.
- Clearly shown in the following screenshot:

  **<img width="476" height="213" alt="h4-Task-d1" src="https://github.com/user-attachments/assets/196bf926-e7c7-46c2-82bc-6f7512873b93" />**

## 2. SELECT from World
### Subtask 1
I executed a basic **SELECT** query to retrieve all countries' names, continents, and populations, giving me an overview of the dataset's structure and content, also shsown in the below screenshot.

### Subtask 2
I applied the **WHERE** clause with a population filter (`>= 200000000`) to list only large countries, practicing numerical comparisons in SQL, can be seen in the following screenshot:

**<img width="594" height="334" alt="h4-Task-d2" src="https://github.com/user-attachments/assets/23c308ce-aef8-4746-8223-f2aa2ed49916" />**

## Reference
sqlzoo.net. (n.d.). *SQLZOO.*  
Available at: https://sqlzoo.net/wiki/SQL_Tutorial.

---

# e) PortSwigger Labs - SQL Injection in WHERE Clause
This lab demonstrated a SQL injection vulnerability in a product category filter. The application inserted user-supplied input directly into a SQL `WHERE` clause without sanitization or parameterization. 
By modifying the gift category parameter, it was possible to alter the logic of the query and retrieve hidden or unreleased products. This reflects both an injection flaw and a broken access-control issue.

## How I Found the Vulnerability
- I noticed that the `category` parameter in the URL (e.g., `?category=Gifts`) influenced the products displayed on the page.
- I injected a syntax-breaking character to test how the server handled unexpected input.
- The application returned a SQL error, confirming that the input was being passed directly into a database query without sanitization.
- This error validated the injection point and allowed further exploitation.

## Anatomy of the Exploit

### **Payload Entry Point**
The vulnerable parameter was the `category` value in the HTTP GET request. This value was inserted directly into the server‑side SQL query.

### **Payload Purpose**
The goal was to:
1. Terminate the original string or expression.
2. Inject a condition that always evaluates to true.
3. Comment out the rest of the query to bypass filters.

The payload used:
' OR 1=1--

### **Why It Worked**

```sql
The server constructed a query similar to:
SELECT * FROM products WHERE category = '<userInput>' AND released = 1;
When I supplied:
' OR 1=1--
the query became:
SELECT * FROM products WHERE category = '' OR 1=1--' AND released = 1;
OR 1=1 makes the condition always true.
-- comments out the remaining clause (AND released = 1), removing the access‑control restriction.
```
As a result, all products, including hidden ones, were returned.

**<img width="836" height="350" alt="h4-Task-e" src="https://github.com/user-attachments/assets/1b3b7cd0-ddfa-42c0-9822-bc8e86c07829" />**

### Defensive Measures & Mitigations (Martinez, 2024)
- Use parameterized queries to ensure user input cannot alter SQL structure.
- Apply strict allow-list validation for parameters like category names.
- Limit database permissions so the application account can only perform necessary operations.

#### Reflection:
This lab highlighted how a single unsanitized parameter can compromise an entire application. It reinforced that security must be built into the foundation of the codebase rather than added as an afterthought. 
Even a simple payload like ' OR 1=1-- can completely bypass access controls when input handling is weak.

##### References
- Martinez, J. (2024). How to Prevent SQL Injection Attacks: 6 Proven Methods.  
  Available at: https://www.strongdm.com/blog/how-to-prevent-sql-injection-attacks
- PortSwigger Web Security Academy. (n.d.). Lab: SQL injection vulnerability in WHERE clause allowing retrieval of hidden data.  
  Available at: https://portswigger.net/web-security/sql-injection/lab-retrieve-hidden-data






