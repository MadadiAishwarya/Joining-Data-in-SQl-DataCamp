Union:
-- Select fields from 2010 table
select *
  -- From 2010 table
  from economies2010
	-- Set theory clause
	Union
-- Select fields from 2015 table
select  *
  -- From 2015 table
  from economies2015
-- Order by code and year
order by code, year;


Union (2):
-- Select field
select country_code
  -- From cities
  from cities
	-- Set theory clause
	Union
-- Select field
select code
  -- From currencies
  from currencies
-- Order by country_code
order by country_code;


Union all:
-- Select fields
SELECT code, year
  -- From economies
  FROM economies
	-- Set theory clause
	union all
-- Select fields
SELECT country_code, year
  -- From populations
  FROM populations
-- Order by code, year
ORDER BY code, year;


Intersect:
-- Select fields
select code,year
  -- From economies
  from economies
	-- Set theory clause
	intersect
-- Select fields
select country_code,year
  -- From populations
  from populations
-- Order by code and year
order by code,year;


Intersect (2):
-- Select fields
select name
  -- From countries
  from countries
	-- Set theory clause
	intersect
-- Select fields
select name
  -- From cities
  from cities;
  
  
Review union and intersect:
UNION: returns all records (potentially duplicates) in both tables


Except:
-- Select field
SELECT name
  -- From cities
  FROM cities
	-- Set theory clause
	except
-- Select field
SELECT capital
  -- From countries
  FROM countries
-- Order by result
ORDER BY name;


Except (2):
-- Select field
select capital
  -- From countries
  from countries
	-- Set theory clause
	except
-- Select field
select name
  -- From cities
  from cities
-- Order by ascending capital
order by capital;


Semi-join:
-- Select code
select code
  -- From countries
  from countries
-- Where region is Middle East
where region='Middle East';

/*
SELECT code
  FROM countries
WHERE region = 'Middle East';
*/

-- Select field
SELECT DISTINCT name
  -- From languages
  FROM languages
-- Order by name
ORDER BY name;

-- Select distinct fields
SELECT DISTINCT name
  -- From languages
  FROM languages
-- Where in statement
WHERE code IN
  -- Subquery
  (SELECT code
   FROM countries
   WHERE region = 'Middle East')
-- Order by name
ORDER BY name;


Relating semi-join to a tweaked inner join:DISTINCT


Diagnosing problems using anti-join:
-- Select statement
select count(name)
  -- From countries
  from countries
-- Where continent is Oceania
where continent='Oceania';

-- 5. Select fields (with aliases)
select c1.code,name, basic_unit as currency
  -- 1. From countries (alias as c1)
  from countries as c1
  	-- 2. Join with currencies (alias as c2)
  	inner join currencies as c2
    -- 3. Match on code
    on c1.code=c2.code
-- 4. Where continent is Oceania
where continent='Oceania';

-- 3. Select fields
SELECT code, name
  -- 4. From Countries
  FROM countries
  -- 5. Where continent is Oceania
  WHERE continent = 'Oceania'
  	-- 1. And code not in
  	AND code NOT IN
  	-- 2. Subquery
  	(SELECT code
  	 FROM currencies);
     
  
Set theory challenge:
-- Select the city name
select name
  -- Alias the table where city name resides
  from  cities AS c1
  -- Choose only records matching the result of multiple set theory clauses
  WHERE country_code IN 
(
    -- Select appropriate field from economies AS e
    SELECT e.code
    FROM economies AS e
    -- Get all additional (unique) values of the field from currencies AS c2  
    union
    SELECT c2.code
    FROM currencies AS c2
    -- Exclude those appearing in populations AS p
    except
    SELECT p.country_code
    FROM populations AS p
);

