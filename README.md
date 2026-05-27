# Basic SQL queries given two tables of example patient info:

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

Both tables have the same numbered ID numbers associated with people/patients and let's assume each ID from both tables corresponds to the same person

Notice the ID numbers are in order from least to greatest in People, but are not in any particular order in Patients.
To align info corresponding to the same ID value in both tables we use the keyword: ON  

Join both tables into one complete view of all patient information:

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

The PatientInfo unified view now looks like this:

### Patient Info


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

"Patient Info" now looks like:

### Patient Info


| ID | Name | Age | Height | Weight | Blood_type |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 2 | Jenny Person | 24 | 205 | 90 | A |
| 3 | Tamir Man | 22 | 180 | 98 | A |
| 4 | Allen Park | 40 | 172 | 87 | A |

## Task 3: Select all patients whose Blood_type is A, who is below the age of 30.

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

"Patient Info" now looks like:

### Patient Info


| ID | Name | Age | Height | Weight | Blood_type |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 2 | Jenny Person | 24 | 205 | 90 | A |
| 3 | Tamir Man | 22 | 180 | 98 | A |

## Task 4: Select all patients whose last name is 'Park'.

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
WHERE People.Name LIKE '%Park';
```

The result now looks like:


| ID | Name | Age | Height | Weight | Blood_type |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 4 | Allen Park | 40 | 172 | 87 | A |
| 6 | Sally Park | 31 | 168 | 60 | null |

LIKE "%Park" means we are searching for a name value that begins with any string of characters followed by the exact string 'Park'. 

Another way of isolating the same two patients would be using LIKE "%Park%" which would select any row with a name that contains 'Park'.


## Task 5: Select any patient whose blood_type value is null.

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

If the request was for patients with non-null blood types you can add a NOT before NULL

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

Sort by Age: in ascending order:

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


Sort by Age: in descending order:

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
