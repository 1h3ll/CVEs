**Project Name & Repo URL:**
[ Medicalcard Generations System](https://phpgurukul.com/medical-card-generation-system-using-php-and-mysql/)

**Vulnerability Type:**
Privilege Escalation via Blind XSS

**Affected Version(s):** v1.0

**💣Vulnerability Description:**

A stored blind XSS vulnerability exists in the Contact Page of the Medical Card Generation System `mcgs/contact.php`. The name field fails to properly sanitize user input, allowing an attacker to inject malicious JavaScript. This payload is stored in the backend and is executed when an admin views the contact submission, making this a blind XSS scenario from the attacker's perspective.
![image](https://github.com/user-attachments/assets/466134f5-2fd5-4e1e-8429-4fbb13aeee37)

**👩‍💻Impact:**
Full admin account takeover, access to sensitive data, and system manipulation.

**🛜Proof-of-Concept (PoC)**
1) There was contact page, where a user can send message to admin.
2) Fill out the form with a Blind XSS payload in **Name** Field and Submit the Form.
![1](https://github.com/user-attachments/assets/0ab4b99b-e6e4-4790-8bff-0322bd13d504)
3) When the admin view the message, the Blind XSS payload will get trigged.
![3](https://github.com/user-attachments/assets/79727dce-23a5-4f0f-a2bd-ddc1d5981dc8)
![4](https://github.com/user-attachments/assets/99d4dbca-20a6-4b0d-9372-4548c3f120f9)
4) View the Response of the Blind XSS Payload, which contains admin **Session-Cookie**.
![5](https://github.com/user-attachments/assets/7b10eed3-4bf2-4f92-959e-a2788898b536)
5) Use the admin cookie to escalate the privilege.
![6](https://github.com/user-attachments/assets/1cc1e47a-1432-44be-8816-76c2dab2dc19)
![7](https://github.com/user-attachments/assets/0021e1ac-37cd-43d7-a00e-2cf9374086fb)

**Recommendation:**
Sanitize input, apply output encoding, and implement CSP.
