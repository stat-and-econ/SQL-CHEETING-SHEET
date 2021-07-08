# SQL Cheeting Sheet

## SQLZOO

https://sqlzoo.net/

GROUP BY & HAVING

```sql
SELECT continent FROM world
GROUP BY continent
HAVING SUM(population) > 100000000
```

COALESCE

```sql
SELECT name, COALESCE(mobile, '07986 444 2266')
FROM teacher
```

SELF JOIN

```sql
SELECT DISTINCT a.company, a.num FROM route a, route b
WHERE a.num = b.num
AND a.company = b.company
AND a.stop = (SELECT id FROM stops WHERE name = 'Craiglockhart')
AND b.stop = (SELECT id FROM stops WHERE name = 'Tollcross')
```

COMPLEX

```sql
SELECT DISTINCT S.num, S.company, stops.name, E.num, E.company
FROM
(SELECT a.company, a.num, b.stop
 FROM route a JOIN route b ON (a.company=b.company AND a.num=b.num)
 WHERE a.stop=(SELECT id FROM stops WHERE name= 'Craiglockhart')
)S
  JOIN
(SELECT a.company, a.num, b.stop
 FROM route a JOIN route b ON (a.company=b.company AND a.num=b.num)
 WHERE a.stop=(SELECT id FROM stops WHERE name= 'Sighthill')
)E
ON (S.stop = E.stop)
JOIN stops ON(stops.id = S.stop)
```



## PROGRAMMERS

https://programmers.co.kr/learn/challenges

변수 선언

```sql
SET @hour := -1; -- 변수 선언

SELECT (@hour := @hour + 1) as HOUR,
(SELECT COUNT(*) FROM ANIMAL_OUTS WHERE HOUR(DATETIME) = @hour) as COUNT
FROM ANIMAL_OUTS
WHERE @hour < 23
```

CASE WHEN THEN WHEN THEN ELSE END

```sql
SELECT ANIMAL_ID, NAME,
CASE WHEN SEX_UPON_INTAKE LIKE '%SPAYED%' THEN 'O'
WHEN SEX_UPON_INTAKE LIKE '%NEUTERED%' THEN 'O'
ELSE 'X' END AS 중성화
FROM ANIMAL_INS
ORDER BY ANIMAL_ID
```

DATE_FORMAT

```sql
SELECT ANIMAL_ID, NAME, 
DATE_FORMAT(DATETIME, '%Y-%m-%d') AS 날짜
FROM ANIMAL_INS
ORDER BY ANIMAL_ID
```

