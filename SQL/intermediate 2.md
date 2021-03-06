#### 데이터리안_백문이불여일타_SQL 중급 강의 수강 2

RDB, 관계형 데이터 베이스는 JOIN이 필요하다. 

## JOIN

### INNER JOIN 
```sql
/*
--OLD
SELECT * 
FROM Customers
Where CustomerID=90
*/
-- 공통된것 조인 
SELECT *
FROM Orders
	INNER JOIN Customers ON Orders.CustomerID=Customers.CustomerID
    INNER JOIN Shippers ON Orders.shipperID=Shippers.ShipperID
```
- INNER JOIN 여러개 가능
- 현업에서는 CustomerID를 조인할 수 없는 형태 OR 조인 키 컬럼이 다를 수 있음
- 그러면 어떻게 하는가? -> ERD를 알아야함. (고급반에서 다룸)
- [SQL Joins Visualizer](https://sql-joins.leopard.in.ua/) 헷갈리면 참고하기

### OUTER JOIN (LEFT,RIGHT)
![image](https://user-images.githubusercontent.com/89775352/158428446-c438e7e2-f449-4d63-9128-4ce21f7740e6.png)
- 이 INNER JOIN 말고는 다 OUTER JOIN 이라고 생각하면 된다. 


Left : 왼쪽은 다 포함하고, 왼쪽이랑 겹치는 B 출력

![image](https://user-images.githubusercontent.com/89775352/159126986-85571fa3-891f-488f-a29e-a129353712d4.png)

```sql
SELECT * 
FROM Customers
	LEFT JOIN Orders ON Customers.CustomerID = Orders.CustomerID
WHERE OrderID IS NULL

RIGHT JOIN은 딱 이 반대 
-- 보통 LEFT JOIN 기준으로 씀, 둘다 쓰면 헷갈리기 때문
LEFT/RIGHT OUTER JOIN = LEFT/RIGHT JOIN
똑같이 동작함. 
```

문제풀이
```sql
SELECT CITY.NAME 
FROM CITY
    INNER JOIN COUNTRY ON COUNTRY.CODE=CITY.COUNTRYCODE
WHERE COUNTRY.CONTINENT= 'Africa'

--CITY 테이블의 NAME 컬럼 출력해달라 -> CITY.NAME 

SELECT SUM(CITY.POPULATION)
FROM CITY 
    INNER JOIN COUNTRY ON CITY.COUNTRYCODE=COUNTRY.CODE
WHERE COUNTRY.CONTINENT= 'Asia';   
    
-- ON 위치 주의 
```
### SELF JOIN
```sql
DATE_ADD(기준날짜, INTERVAL)
DATE_ADD(NOW(), INTERVAL 1 SECOND)
DATE_ADD(NOW(), INTERVAL 1 MINUTE)
DATE_ADD(NOW(), INTERVAL 1 HOUR)
DATE_ADD(NOW(), INTERVAL 1 DAY)
DATE_ADD(NOW(), INTERVAL 1 MONTH)
DATE_ADD(NOW(), INTERVAL 1 YEAR)

DATE_SUB(기준날짜, INTERVAL 1 DAY)

SELECT *
FROM A AS today 
        INNER JOIN A AS nextday ON DATE_ADD(today.start_date,INTERVAL +1 DAY)=nextday.start_date

-- 서브 쿼리, 셀프 조인 테이블 만들때 마다 칼럼 이름을 AS 로 다르게 지정해주는 게 좋다. 
-- 그렇지 않으면 충돌이 잦다. 
```
