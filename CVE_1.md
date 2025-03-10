# Vulnerability Title
Unauthorized SQL Injection Vulnerability in `security_addUser.jsp` Interface of Zhiyuan Interconnect FE Collaborative Office Platform

---

# Vulnerability Description
The FE Collaborative Office Platform developed by Beijing Zhiyuan Interconnect Software Co., Ltd. contains an SQL injection vulnerability in the `/security/addUser.jsp` interface. The input parameters are not properly filtered, allowing attackers to craft malicious requests that trigger the SQL injection vulnerability. Successfully exploiting this vulnerability can lead to the leakage of sensitive database information (such as user credentials and system configurations). Some verified affected systems have a database user with `sa` (system administrator) privileges, representing a high risk.

---

# Affected Products
+ **Affected Product**: Zhiyuan Interconnect FE Collaborative Office Platform (Note: Not the Feiqi Interconnect products).
+ **Verification Feature**: Potentially affected assets can be identified by searching `app="Zhiyuan Interconnect-FE"` using network space mapping tools like Fofa.

---

# Vulnerability Verification and Reproduction
## Vulnerable Location
```plain
http://[Target IP]:9090/security/addUser.jsp?*******
```

## Reproduction Tool
Automated detection with `sqlmap`:

```bash
sqlmap -u "http://Target IP:9090/security/addUser.jsp?******" --risk=3 --level=5
```

## Verified Cases
1. **Case 1**: `http://125.91.119.**:9090`
    - sqlmap confirms the vulnerability, user is `sa`![](https://cdn.nlark.com/yuque/0/2025/png/40663643/1741592447335-d19640f8-dcfa-4045-91c3-651a9de47257.png)
    - Asset Proof ![](https://cdn.nlark.com/yuque/0/2025/png/40663643/1741595668434-099dd824-c177-446a-b6a5-8e2358b77bb2.png)
2. **Case 2**: `http://218.22.206.**:9090`
    - sqlmap confirms the vulnerability, user is `sa`![](https://cdn.nlark.com/yuque/0/2025/png/40663643/1741592646507-14ed52d0-bd09-4743-bb67-60df60e76fe8.png)
    - Asset Proof ![](https://cdn.nlark.com/yuque/0/2025/png/40663643/1741592702286-0cd01c6c-1c7a-4226-a3c7-67c0a4ba95a4.png)
---

# Proof of Vulnerability
## Vendor Information
+ **Vendor Name**: 北京致远互联软件股份有限公司
+ **Vendor English Name**: BeiJing Seeyon Internet Software Corp.
+ **Vendor Website**: [www.seeyon.com](https://www.seeyon.com/)
+ **Vendor Email**: [zhangxiu@seeyon.com](mailto:zhangxiu@seeyon.com)
+ **Registered Capital**: 115.158439 million RMB
+ ![](https://cdn.nlark.com/yuque/0/2025/png/38476061/1740239688897-2baca77d-ce5c-42ca-820a-30439b29d463.png)

---

## Technical Details
+ **Technical Details**: The `*******` parameter is not filtered, and attackers can inject characters (such as `1*`) to trigger database errors or blind injections.

---

# Remediation Suggestions
1. **Input Filtering**: Implement strict type checks (e.g., force conversion to integers) and filter special characters for parameters such as `*******`.
2. **Prepared Statements**: Use parameterized queries instead of dynamically concatenating SQL queries.
3. **Least Privilege**: Reduce the privileges of the database connection accounts and avoid using high-privilege accounts like `sa`.
4. **Patch and Upgrade**: Contact Zhiyuan Interconnect for security updates or temporary fixes.

---

# Disclaimer
This report is intended for technical research and vulnerability remediation purposes only. It is prohibited for illegal use. Exploiting vulnerabilities to attack others' systems will result in legal consequences.

---

# Appendix
Other affected assets:

```plain
*************
```

