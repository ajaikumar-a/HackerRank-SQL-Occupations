# Occupations

Pivot the Occupation column in OCCUPATIONS so that each Name is sorted alphabetically and displayed underneath its corresponding Occupation. The output column headers should be Doctor, Professor, Singer, and Actor, respectively.
Note: Print NULL when there are no more names corresponding to an occupation.

## Solution:

```
SELECT
  MIN(Doctor), MIN(Professor), MIN(Singer), MIN(Actor)
FROM
  (SELECT
     ROW_NUMBER() OVER(PARTITION BY Occupation ORDER BY Name) rn,
     CASE WHEN Occupation = 'Doctor' THEN Name END AS Doctor,
     CASE WHEN Occupation = 'Professor' THEN Name END AS Professor,
     CASE WHEN Occupation = 'Singer' THEN Name END AS Singer,
     CASE WHEN Occupation = 'Actor' THEN Name END AS Actor
  FROM
    OCCUPATIONS
  ORDER BY 
    Name) c
GROUP BY 
  rn
ORDER BY
  rn;
```
