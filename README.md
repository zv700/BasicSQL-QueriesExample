# Basic SQL queries given two tables of example/mock patient info:

### People


| ID | Name | Age |
| :--- | :--- | :--- |
| 1 | John Man | 35 |
| 2 | Jenny Person | 24 |
| 3 | Tamir Man | 22 |
| 4 | Allen Park | 40 |
| 5 | Alice Green | 58 |
| 6 | Sally Park | 31 |
| 7 | Jamie Blue | 46 |

### Patients


| ID | Height | Weight | Blood_type |
| :--- | :--- | :--- | :--- |
| 2 | 205 | 90 | A |
| 1 | 165 | 70 | O |
| 5 | 155 | 65 | B |
| 7 | null | null | null |
| 3 | 180 | 98 | A |
| 6 | 168 | 60 | null |
| 4 | 172 | 87 | A |

## Task 1: Join both tables so each patient's information is complete.

- Both tables have the same ID numbers associated with people/patients. Let's assume in this example each ID from both tables corresponds to the same person.

- Notice the ID numbers are in order from least to greatest in People, but are not in any particular order in Patients.
To align info corresponding to the same ID value in both tables we use the keyword: ON  

Join columns of both tables into one:

```sql
SELECT 
    People.ID,
    People.Name,
    People.Age,
    Patients.Height,
    Patients.Weight,
    Patients.Blood_type
FROM People
INNER JOIN Patients 
    ON People.ID = Patients.ID;

```

Result:


| ID | Name | Age | Height | Weight | Blood_type |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | John Man | 35 | 165 | 70 | O |
| 2 | Jenny Person | 24 | 205 | 90 | A |
| 3 | Tamir Man | 22 | 180 | 98 | A |
| 4 | Allen Park | 40 | 172 | 87 | A |
| 5 | Alice Green | 58 | 155 | 65 | B |
| 6 | Sally Park | 31 | 168 | 60 | null |
| 7 | Jamie Blue | 46 | null | null | null |

## Task 2: Select all patients whose Blood_type is A.

- We maintain all of the selected columns and specify a specific column's value to search for using: WHERE columnName = 'desiredValue'


```sql
SELECT 
    People.ID,
    People.Name,
    People.Age,
    Patients.Height,
    Patients.Weight,
    Patients.Blood_type
FROM People
INNER JOIN Patients 
    ON People.ID = Patients.ID
WHERE Patients.Blood_type = 'A';
```

Result now looks like:


| ID | Name | Age | Height | Weight | Blood_type |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 2 | Jenny Person | 24 | 205 | 90 | A |
| 3 | Tamir Man | 22 | 180 | 98 | A |
| 4 | Allen Park | 40 | 172 | 87 | A |

## Task 3: Select all patients whose Blood_type is A, who is below the age of 30.

- For columns that have number number values, we can use comparison operators for greater than > or less than <. 

- This task asks for two conditions. We use AND between the two conditions within the WHERE statement because in this situation we are looking for cases where both conditions are true. 

```sql
SELECT 
    People.ID,
    People.Name,
    People.Age,
    Patients.Height,
    Patients.Weight,
    Patients.Blood_type
FROM People
INNER JOIN Patients 
    ON People.ID = Patients.ID
WHERE Patients.Blood_type = 'A'
	AND People.Age < 30;
```

Result now looks like:


| ID | Name | Age | Height | Weight | Blood_type |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 2 | Jenny Person | 24 | 205 | 90 | A |
| 3 | Tamir Man | 22 | 180 | 98 | A |

## Task 4: Select all patients whose last name is 'Park'.

- LIKE '%park' means we are searching for a name value that begins with any string of characters followed by the string 'park'. Case sensitivity of the single quoted term in that follows LIKE depends on the specific SQL system being used.

- Another way of isolating the same two patients would be using LIKE "%park%" which would select any row with a name that contains 'park'. While it would work in this situation, it would not be ideal in every situation because it would also include any patients who have the sequence of characters in "park" within their first name.

Query: uses WHERE columnName LIKE '%searchTerm%'

```sql
SELECT 
    People.ID,
    People.Name,
    People.Age,
    Patients.Height,
    Patients.Weight,
    Patients.Blood_type
FROM People
INNER JOIN Patients 
    ON People.ID = Patients.ID
WHERE People.Name LIKE '%park';
```

The result now looks like:


| ID | Name | Age | Height | Weight | Blood_type |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 4 | Allen Park | 40 | 172 | 87 | A |
| 6 | Sally Park | 31 | 168 | 60 | null |



## Task 5: Select any patient whose blood_type value is null.

Query: uses WHERE columnName IS NULL

```sql
SELECT 
    People.ID,
    People.Name,
    People.Age,
    Patients.Height,
    Patients.Weight,
    Patients.Blood_type
FROM People
INNER JOIN Patients 
    ON People.ID = Patients.ID
WHERE Patients.Blood_type IS NULL;
```

The result now looks like:


| ID | Name | Age | Height | Weight | Blood_type |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 6 | Sally Park | 31 | 168 | 60 | null |
| 7 | Jamie Blue | 46 | null | null | null |

- If the request was for patients with non-null blood types you can add a NOT before NULL.

Query: uses WHERE columnName IS NOT NULL

```sql
SELECT 
    People.ID,
    People.Name,
    People.Age,
    Patients.Height,
    Patients.Weight,
    Patients.Blood_type
FROM People
INNER JOIN Patients 
    ON People.ID = Patients.ID
WHERE Patients.Blood_type IS NOT NULL;
```

The result now looks like:


| ID | Name | Age | Height | Weight | Blood_type |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | John Man | 35 | 165 | 70 | O |
| 2 | Jenny Person | 24 | 205 | 90 | A |
| 3 | Tamir Man | 22 | 180 | 98 | A |
| 4 | Allen Park | 40 | 172 | 87 | A |
| 5 | Alice Green | 58 | 155 | 65 | B |



## Task 6: Sort the patients by Age: ascending and descending.

- ORDER BY is used to sort rows by ascending ASC or descending DESC

- If the column contains numbers, ASC sorts the numbers from least to greatest and DESC sorts the numbers from greatest to least.

- If the column contains a string of letters, ASC sorts from A to Z (alphabetical order) and DESC sorts from Z to A (reverse alphabetical order). 

Query: Sort by Age in ascending order (least to greatest) -> ORDER BY columnName ASC

```sql
SELECT 
    People.ID,
    People.Name,
    People.Age,
    Patients.Height,
    Patients.Weight,
    Patients.Blood_type
FROM People
INNER JOIN Patients 
    ON People.ID = Patients.ID
ORDER BY People.Age ASC;
```

The result now looks like:


| ID | Name | Age | Height | Weight | Blood_type |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 3 | Tamir Man | 22 | 180 | 98 | A |
| 2 | Jenny Person | 24 | 205 | 90 | A |
| 6 | Sally Park | 31 | 168 | 60 | null |
| 1 | John Man | 35 | 165 | 70 | O |
| 4 | Allen Park | 40 | 172 | 87 | A |
| 7 | Jamie Blue | 46 | null | null | null |
| 5 | Alice Green | 58 | 155 | 65 | B |


Query: Sort by Age in descending order (greatest to least) -> ORDER BY columnName DESC

```sql
SELECT 
    People.ID,
    People.Name,
    People.Age,
    Patients.Height,
    Patients.Weight,
    Patients.Blood_type
FROM People
INNER JOIN Patients 
    ON People.ID = Patients.ID
ORDER BY People.Age DESC;
```

The result now looks like:


| ID | Name | Age | Height | Weight | Blood_type |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 5 | Alice Green | 58 | 155 | 65 | B |
| 7 | Jamie Blue | 46 | null | null | null |
| 4 | Allen Park | 40 | 172 | 87 | A |
| 1 | John Man | 35 | 165 | 70 | O |
| 6 | Sally Park | 31 | 168 | 60 | null |
| 2 | Jenny Person | 24 | 205 | 90 | A |
| 3 | Tamir Man | 22 | 180 | 98 | A |
