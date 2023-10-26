# Football Matches - Tasks

Each of the questions/tasks below can be answered using a `SELECT` query. When you find a solution copy it into the code block under the question before pushing your solution to GitHub.

1) Find all the matches from 2017.

```sql
SELECT COUNT(*) FROM matches WHERE season='2017';
7810
```

2) Find all the matches featuring Barcelona.

```sql
SELECT COUNT(*) FROM matches WHERE awayteam = 'Barcelona' OR hometeam = 'Barcelona';
608
SELECT * FROM matches WHERE awayteam = 'Barcelona' OR hometeam = 'Barcelona';
608

```

3) What are the names of the Scottish divisions included?

```sql
SELECT name FROM divisions WHERE country='Scotland'
Scottish Premiership
Scottish Championship
Scottish League One
```

4) Find the value of the `code` for the `Bundesliga` division. Use that code to find out how many matches Freiburg have played in that division. HINT: You will need to query both tables

```sql
SELECT code FROM divisions WHERE name='Bundesliga';
SELECT COUNT(*)from matches WHERE division_code='D1' AND (hometeam='Freiburg' OR awayteam='Freiburg');
∴ 374 
```

5)  Find the teams which include the word "City" in their name. HINT: Not every team has been entered into the database with their full name, eg. `Norwich City` are listed as `Norwich`. If your query is correct it should return four teams.

```sql
SELECT DISTINCT hometeam  FROM matches WHERE hometeam LIKE '% City'; 
Bath City
Man City
Edinburgh City
Bristol City
****
```

6) How many different teams have played in matches recorded in a French division?

```sql
SELECT code FROM divisions WHERE country='France';

SELECT COUNT(DISTINCT hometeam)  FROM matches WHERE division_code='F1' OR division_code='F2'; 
61
```

7) Have Huddersfield played Swansea in any of the recorded matches?

```sql
SELECT COUNT(*)
FROM Matches
WHERE
(hometeam = 'Huddersfield' AND
awayteam = 'Swansea')
OR
(hometeam = 'Swansea' AND
awayteam = 'Huddersfield');
∴ YES
```

8) How many draws were there in the `Eredivisie` between 2010 and 2015?

```sql
SELECT COUNT(*) FROM matches WHERE (division_code='N1' AND ftr='D') and (season > 2009 and season < 2016);
431
```

9) Select the matches played in the Premier League in order of total goals scored (`fthg` + `ftag`) from highest to lowest. When two matches have the same total the match with more home goals (`fthg`) should come first. 

```sql
SELECT * FROM matches WHERE division_code='E0' ORDER BY (fthg+ftag) DESC;
100988	E0	Portsmouth	Reading	7	4	H	2008
69944	E0	Man United	Arsenal	8	2	H	2012
62363	E0	Arsenal	Newcastle	7	3	H	2013
etc.
```

10) Find the name of the division in which the most goals were scored in a single season and the year in which it happened.

```sql
SELECT (Count(ftag)) + (Count(fthg)) as total, season, division_code from matches group by division_code, season ORDER BY total DESC limit 1;
SELECT name from divisions where code ='E1';
∴ EFL Championship 2007
```

### Useful Resources

- [Filtering results](https://www.w3schools.com/sql/sql_where.asp)
- [Ordering results](https://www.w3schools.com/sql/sql_orderby.asp)
- [Grouping results](https://www.w3schools.com/sql/sql_groupby.asp)
