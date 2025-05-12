**[Stored Cross-Site Scripting (XSS)] in [User Registration & Login and User Management System with Admin Panel] <= v1.0
BUG Author: Girish**

**Product Information:**
Vendor: PHPGurukul
Project Page: https://phpgurukul.com/user-registration-login-and-user-management-system-with-admin-panel/
Affected Version: ≤ v1.0
Tested On: Localhost (http://localhost/loginsystem/)

**Vulnerability Details:**
Type: Stored Cross-Site Scripting (XSS)
CWE ID: CWE-79
Severity: HIGH (CVSS 3.1 Score: 8.0)
Attack Vector: Remote, Persistent

**Affected Components:**
signup.php (input)
admin/dashboard.php (payload reflected)

**Root Cause:**
User-controlled input (First Name, Last Name) is not sanitized or encoded before being displayed in the Total Registered Users section of the Admin Dashboard, leading to persistent XSS when the admin logs in.

**Proof of Concept:**
Navigate to http://localhost/loginsystem/signup.php
Enter the following into the First Name or Last Name field:
girish"><img src=x onerror=alert(1)>
Complete registration.
Login as admin and open http://localhost/loginsystem/admin/dashboard.php
A JavaScript alert (alert(1)) is triggered, proving the stored XSS.

**Attack Vector:**
An attacker registers with a malicious XSS payload. Once the admin logs in and visits the dashboard, the script executes in their browser context, potentially allowing:

Session hijacking
Admin panel manipulation
Data theft or tampering

**Recommendations:**
Use htmlspecialchars() or a similar function to encode all dynamic content.
Validate and sanitize all user input on both client and server sides.
Employ a Content Security Policy (CSP) to limit inline/external script execution.





