# Web-Application-Testing-Lab2

# SQL inJection Lab

The objective in this lab is to identify and exploit a Union SQL Injection vulnerability present in the ID parameter of the /about/ID endpoint of a Web application. By leveraging this vulnerability, with the help of Burp Suite, an attack to retrieve the notes about the CEO stored in the database.


# Skills Learned
- Setting up and Configuring Burp Suite: configuring the Burp Suite proxy settings to intercept HTTP/HTTPS traffic
- Intercepting and Manipulating HTTP Requests: capturing requests and responses with the Proxy tool.
- Modifying  request parameters,headers, and cookies for manual testing.
- Runing scans to detect common web vulnerabilities like SQL injection, XSS, and CSRF.
- Testing session management to identify insecure session handling and cookie weakness.
- Manual vulnerability Testing with Repeater.Repeating and modifying requests to test for SQLi,XSS and other input-based vulnerabilities.
- Using Intruder to brute-force login and bypass authentication.
- Utilizing the Target tool to map the web application's endpoints and understand its structure.
- Learning about secure coding practices to mitigate identified vulnerabilities.
- Documenting vulnerabilities,their impact, and their potential remediation.
- Exporting reports and organinizing findings for stakeholders.


# Tools Used

- Burp Suite Community Edition is used for Web application Penetration Vulnerability testing. A very powerful tool for Web application security testing,SQLi, XSS,CSRFintercept request,modify them,craft payloads.


# Steps

Fig1: An image showing a website being tested for SQL injection, with the focus on the CEO profile page, which is identified as the target for testing.
![Capture](https://github.com/user-attachments/assets/a16fb162-bdaa-4118-8008-92f99cfcb08f)


Fig2: Burp Suite Proxy is used to intercept the request and Foward it back to the repeater.
![Capture](https://github.com/user-attachments/assets/1b2d02fe-304a-4ac6-8a55-8a7152f6340d)


Fig3: An image showing the confirmation of an SQL vulnerability by adding a single apostrophe (') to the `/about/2` path in the request view. The response view displays confirmation of the vulnerability.
![Capture](https://github.com/user-attachments/assets/7fd27d99-5681-4734-b1b9-b839a2908ba4)


The message tells us a couple of things that will be invaluable when exploiting this vulnerability:

The database table we are selecting from is called people.
The query selects five columns from the table: firstName, lastName, pfpLink, role, and bio.

Fig4: An image demonstrating the retrieval of all information from the "people" table using the command `/about/0 UNION ALL SELECT group_concat(column_name), null, null, null, null FROM information_schema.columns WHERE table_name="people"`. The request view displays complete information about the table.
![Capture](https://github.com/user-attachments/assets/831ca78e-f1a3-4146-ab5f-306b2b7e4617)

Fig5: An image showing the successful identification of eight columns in the table: `id`, `firstName`, `lastName`, `pfpLink`, `role`, `shortRole`, `bio`, and `notes`. A crafted query, `0 UNION ALL SELECT notes, null, null, null, null FROM people WHERE id = 1`, is used to extract information from the database.
![Capture](https://github.com/user-attachments/assets/aa78dc3a-8e39-44bf-b3ef-6040d1564ce0)

# Note
By using SQL injection and Burp Suite, we successfully retrieved the data stored in the database: THM{ZGE3OTUyZGMyMzkwNjJmZjg3Mzk1NjJh}.
