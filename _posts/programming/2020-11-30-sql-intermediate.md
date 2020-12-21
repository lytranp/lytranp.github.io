---
layout: post
mathjax: true
title: "SQL - Intermediate - Part 1"
read: 15
secondary: others
date: 2020-11-30
---

### 1. CASE statements
![](/sources/sql-intermediate.png){:height="60%" width="60%"}

![](/sources/sql-intermediate3.png){:height="60%" width="60%"}

![](/sources/sql-intermediate4.png){:height="60%" width="60%"}

**a. CASE - basic**

```-sql
SELECT 
    CASE WHEN hometeam_id = 1089 THEN 'FC Schalke 04'
         WHEN hometeam_id = 9823 THEN 'FC Bayern Munich'
    ELSE 'Other' 
    END AS home_team,
    COUNT(id) AS total_matches
FROM matches_germany
GROUP BY home_teams;
```
![](/sources/sql-intermediate2.png){:height="60%" width="60%"}

**b. CASE - compare column values**

```-sql
SELECT 
	-- Select the date of the match
	date,
	-- Identify home wins, losses, or ties
	CASE WHEN home_goal > away_goal THEN 'Home win!'
        WHEN home_goal < away_goal THEN 'Home loss :(' 
        ELSE 'Tie' END AS outcome
FROM matches_spain;
```
 
Table **teams_spain**: 
+ Information of away team
+ team_api_id: match with **awayteam_id** of table **matches_spain**

Table **teams_spain**: 
+ Information of match between **hometeam_id** and **awayteam_id**

```-sql
SELECT m.date
       ,t.team_long_name AS opponent
       ,CASE WHEN m.home_goal > away_goal THEN 'Barcelona win!'
            WHEN m.home_goal > away_goal THEN 'Barcelona loss'
        ELSE 'Tie' END AS outcome
FROM matches_spain AS m
LEFT JOIN teams_spain AS t
ON m.awayteam_id = t.team_api_id
-- Filter for Barcelona as the home team
WHERE m.hometeam_id = 8634;
```

*Problem*: List matches between FC Barcelona(id = 8634) and Real Madrid CF (id = 8633)

```-sql
SELECT date
       ,CASE WHEN hometeam_id = 8634 THEN 'FC Barcelona'
             WHEN hometeam_id = 8633 THEN 'Real Madrid CF'
        ELSE 'Tie' END AS home
        ,CASE WHEN awayteam_id = 8634 THEN 'FC Barcelona'
             WHEN awayteam_id = 8633 THEN 'Real Madrid CF'
        ELSE 'Tie' END AS away
FROM matches_spain
--Condition: hard because just want to filter Barcelona with Real (and vice versa), not Barcelona with other teams
WHERE (hometeam_id = 8634 OR awayteam_id = 8634)
AND (awayteam_id = 8633 OR hometeam_id = 8633);
```
![](/sources/sql-intermediate5.png){:height="60%" width="60%"}

*Problem*: improve a bit from above problem 
```-sql
SELECT date
       ,CASE WHEN hometeam_id = 8634 THEN 'FC Barcelona'
             WHEN hometeam_id = 8633 THEN 'Real Madrid CF'
        ELSE 'Tie' END AS home
        ,CASE WHEN awayteam_id = 8634 THEN 'FC Barcelona'
             WHEN awayteam_id = 8633 THEN 'Real Madrid CF'
        ELSE 'Tie' END AS away
        ,CASE WHEN home_goal > away_goal AND hometeam_id = 8634 THEN 'Barcelona wins'
            WHEN home_goal > away_goal AND hometeam_id = 8633 THEN 'Real Madrid win!'
            WHEN home_goal < away_goal AND awayteam_id = 8634 THEN 'Barcelona wins'
            WHEN home_goal < away_goal AND awayteam_id = 8633 THEN 'Real Madrid win!'
        ELSE 'Tie' END AS outcome
FROM matches_spain
WHERE (hometeam_id = 8634 OR awayteam_id = 8634)
AND (awayteam_id = 8633 OR hometeam_id = 8633);
```
![](/sources/sql-intermediate6.png){:height="60%" width="60%"}

**c. Filter CASE**

Example

Step 1: Filter team = 'Bologna'

```sql
SELECT
	team_long_name,
	team_api_id
FROM teams_italy
WHERE team_long_name = 'Bologna';
```

Step 2: Identify when Bologna won a match

```sql
SELECT
	season,
	date,
    CASE WHEN hometeam_id = 9857 AND home_goal > away_goal THEN 'Bologna Win'
        WHEN awayteam_id = 9857 AND away_goal > home_goal THEN 'Bologna Win'
    END AS outcome
FROM matches_italy;
```
![](/sources/sql-intermediate7.png){:height="60%" width="60%"}


Step 3: Filter outcome "Bologna wins"

```sql
SELECT
	season,
	date,
    home_goal,
    away_goal,
    CASE WHEN hometeam_id = 9857 AND home_goal > away_goal THEN 'Bologna Win'
        WHEN awayteam_id = 9857 AND away_goal > home_goal THEN 'Bologna Win'
    END AS outcome
FROM matches_italy
WHERE
    (CASE WHEN hometeam_id = 9857 AND home_goal > away_goal THEN 'Bologna Win'
        WHEN awayteam_id = 9857 AND away_goal > home_goal THEN 'Bologna Win'
    END) IS NOT NULL;
```
![](/sources/sql-intermediate8.png){:height="60%" width="60%"}

d. CASE with aggregate function 

*Problem*: Count games in the 2012/2013 season

```sql
SELECT season,
	COUNT(CASE WHEN m.season = '2012/2013' 
        	THEN m.id ELSE NULL END) AS matches_2012_2013
FROM match AS m
GROUP BY season;
```

*Problem*: Count games in the 2012/2013, 2013/2014 season

```sql
SELECT c.name,
	COUNT(CASE WHEN m.season = '2012/2013' 
        	THEN m.id ELSE NULL END) AS matches_2012_2013
    ,COUNT(CASE WHEN m.season = '2013/2014'
            THEN m.id END) AS matches_2013_2014
FROM match AS m
LEFT JOIN country AS c
ON c.id = m.country_id
GROUP BY c.name;
```

E. CASE with aggregate function 

General formula
```
AVG(CASE WHEN condition_is_met THEN 1
         WHEN condition_is_not_met THEN 0 END)
```

*Problem*: Compute average score of matches in each country and each season

```sql
SELECT 
	c.name AS country,
    -- Calculate the percentage of tied games in each season
	AVG(CASE WHEN m.season= '2013/2014' AND m.home_goal = m.away_goal THEN 1
			 WHEN m.season= '2013/2014' AND m.home_goal != m.away_goal THEN 0
			 END) AS ties_2013_2014,
	AVG(CASE WHEN m.season= '2014/2015' AND m.home_goal = m.away_goal THEN 1
			 WHEN m.season= '2014/2015' AND m.home_goal != m.away_goal THEN 0
			 END) AS ties_2014_2015
FROM country AS c
LEFT JOIN matches AS m
ON c.id = m.country_id
GROUP BY country;
```

![](/sources/sql-intermediate9.png){:height="60%" width="60%"}

Please read [SQL - Intermediate - Part 2](2011-11-30-sql-intermediate2.md)