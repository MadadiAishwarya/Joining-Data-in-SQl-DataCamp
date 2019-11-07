Inner join:
-- Select all columns from cities
Select *  from cities

SELECT * 
FROM cities
  -- 1. Inner join to countries
  INNER JOIN countries
    -- 2. Match on the country codes
    ON cities.country_code = countries.code;
    
 -- 1. Select name fields (with alias) and region 
SELECT cities.name as city, countries.name as country, countries.region 
FROM cities
  INNER JOIN countries
    ON cities.country_code = countries.code;
    
 
Inner join (2):
-- 3. Select fields with aliases
SELECT c.code AS country_code, name, year,inflation_rate
FROM countries AS c
  -- 1. Join to economies (alias e)
  inner JOIN economies as e
    -- 2. Match on code
    ON c.code = e.code;
    
   
Inner join (3):
-- 4. Select fields
select code,name,region,year,fertility_rate
  -- 1. From countries (alias as c)
  from countries as c
  -- 2. Join with populations (as p)
  inner join populations as p
    -- 3. Match on country code
    on c.code=p.country_code
    
 -- 6. Select fields
SELECT c.code, name, region, e.year, fertility_rate,unemployment_rate
  -- 1. From countries (alias as c)
  FROM countries AS c
  -- 2. Join to populations (as p)
  INNER JOIN populations AS p
    -- 3. Match on country code
    ON c.code = p.country_code
  -- 4. Join to economies (as e)
  inner join economies as e
    -- 5. Match on country code
   on c.code = e.code;
   
-- 6. Select fields
SELECT c.code, name, region, e.year, fertility_rate, unemployment_rate
  -- 1. From countries (alias as c)
  FROM countries AS c
  -- 2. Join to populations (as p)
  INNER JOIN populations AS p
    -- 3. Match on country code
    ON c.code = p.country_code
  -- 4. Join to economies (as e)
  INNER JOIN economies AS e
    -- 5. Match on country code and year
    on c.code=e.code and
    p.year=e.year;
    
    
Review inner join using on:INNER JOIN requires a specification of the key field (or fields) in each table.


Inner join with using:
-- 4. Select fields
select c.name as country,continent,l.name as language,official
  -- 1. From countries (alias as c)
  from countries as c
  -- 2. Join to languages (as l)
  inner join languages as l
    -- 3. Match using code
    using(code)
    
    
 Self-join:
-- 4. Select fields with aliases
select p1.country_code,
p1.size as size2010,
p2.size as size2015
-- 1. From populations (alias as p1)
from populations as p1
  -- 2. Join to itself (alias as p2)
  inner join populations as p2
    -- 3. Match on country code
    on p1.country_code=p2.country_code
    
-- 5. Select fields with aliases
SELECT p1.country_code,
       p1.size AS size2010,
       p2.size AS size2015
-- 1. From populations (alias as p1)
FROM populations as p1
  -- 2. Join to itself (alias as p2)
  inner JOIN populations as p2
    -- 3. Match on country code
    ON p1.country_code = p2.country_code
        -- 4. and year (with calculation)
        and p1.year=p2.year-5
  
SELECT p1.country_code,
       p1.size AS size2010, 
       p2.size AS size2015,
       -- 1. calculate growth_perc
       ((p2.size - p1.size)/p1.size * 100.0) AS growth_perc
-- 2. From populations (alias as p1)
FROM populations AS p1
  -- 3. Join to itself (alias as p2)
  INNER JOIN populations AS p2
    -- 4. Match on country code
    ON p1.country_code = p2.country_code
        -- 5. and year (with calculation)
        AND p1.year = p2.year - 5;
        
        
Case when and then:
SELECT name, continent, code, surface_area,
    -- 1. First case
    CASE WHEN surface_area > 2000000 THEN 'large'
        -- 2. Second case
        WHEN  surface_area > 350000 and surface_area < 2000000 THEN 'medium'
        -- 3. Else clause + end
        ELSE 'small' END
        -- 4. Alias name
        AS geosize_group
-- 5. From table
FROM countries;


Inner challenge:
SELECT country_code, size,
    -- 1. First case
    CASE WHEN size > 50000000 THEN 'large'
        -- 2. Second case
        WHEN size > 1000000 and size < 50000000 THEN 'medium'
        -- 3. Else clause + end
        ELSE 'small' END
        -- 4. Alias name
        AS popsize_group
-- 5. From table
FROM populations
-- 6. Focus on 2015
WHERE year = 2015;

SELECT country_code, size,
    CASE WHEN size > 50000000 THEN 'large'
        WHEN size > 1000000 THEN 'medium'
        ELSE 'small' END
        AS popsize_group
-- 1. Into table
into pop_plus
FROM populations
WHERE year = 2015;
-- 2. Select all columns of pop_plus
select * from pop_plus;

SELECT country_code, size,
  CASE WHEN size > 50000000
            THEN 'large'
       WHEN size > 1000000
            THEN 'medium'
       ELSE 'small' END
       AS popsize_group
INTO pop_plus       
FROM populations
WHERE year = 2015;
-- 5. Select fields
select name,continent,geosize_group,popsize_group
from countries_plus as c
inner join pop_plus as p
on c.code=p.country_code
order by geosize_group;
