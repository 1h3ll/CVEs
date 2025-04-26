**Project Name & Repo URL:**
[Maid Hiring Management System using PHP and MySQL](https://phpgurukul.com/maid-hiring-management-system-using-php-and-mysql/)

**Vulnerability Type:**
Stored XSS

**Affected Version(s):** v1.0

**💣Vulnerability Description:**
A Stored Cross-Site Scripting (XSS) vulnerability exists in the About page editing functionality `(/mcgs/admin/aboutus.php)` of the Medical Card Generation System developed by PHPGurukul. The application does not properly sanitize or encode user-supplied input when updating the About page content.
An authenticated admin (or an attacker who gains access to the edit functionality) can inject arbitrary JavaScript code into the About page. The malicious script is stored in the backend database and is executed whenever a user accesses the About page `(/mcgs/)`.

**👩‍💻Impact:**
Hijack user sessions,
Steal sensitive information,
Perform actions on behalf of authenticated users,
Redirect users to malicious websites,
Escalate privileges within the application.

**🛜Proof-of-Concept (PoC):**

1)Login into an admin account and view the endpoint `/mcgs/admin/aboutus.php`.

2)Inject a XSS script `"><script>alert('XSS')</script>`.
![1](https://github.com/user-attachments/assets/47852503-a12a-4477-994d-e350ab81db2b)

3)View the home page `/mcgs/`.
![2](https://github.com/user-attachments/assets/38b8d01f-d53f-4a0f-88bb-80ac0b258c21)

**Recommendation:**

Sanitize input, apply output encoding, and implement CSP.
