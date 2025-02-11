# Datum-Tech-Academic-Data-Analysis
Datum Tech faces several challenges that require a detailed analysis of its academic data. They recently moved their data to a database and need a data analyst to manipulate it and extract meaningful insight.

## 🏫 Project Overview
Datum Tech is a leading data platform known for its academic technological excellence. They offer a variety of programs across multiple departments. However, they face challenges in managing and analyzing student performance, course popularity, and departmental insights. This SQL-based analysis provides actionable insights to improve student success and optimize course distribution.

## 🎯 Objectives
- Identify patterns in student performance to enhance learning outcomes.
- Analyze course distribution across departments.
- Provide insights for better resource allocation and academic planning.

## 📝 Dataset
The dataset consists of the following key tables:
- **`students`**: Contains student details.
- **`departments`**: Lists all academic departments.
- **`courses`**: Contains course details and department associations.
- **`scores`**: Records student performance in different courses.
- **`teachers`**: Stores teacher details including salary.

## 🔍 SQL Analysis & Queries

#### 🔹 How many departments are in Datum Tech?
```sql
SELECT COUNT(DISTINCT department_id) FROM departments;
```
#### 🔹 Number of courses available in each department
```sql
SELECT department, COUNT(DISTINCT course_id) AS total_courses 
FROM courses
GROUP BY department;
```
#### 🔹 Courses offered in the 'MS Excel' department
```sql
SELECT course_name, department 
FROM courses 
WHERE department = 'DP1';
```
#### 🔹 Identify students who scored more than 70 in any course
```sql
SELECT student_name, score 
FROM scores 
WHERE score > 70;
```
#### 🔹 Calculate the average score of all students in 'Advanced Excel'
```sql
SELECT ROUND(AVG(score), 2) AS avg_score 
FROM scores 
WHERE course_id = 'EX103';
```
#### 🔹 Top 20 students across all courses based on score
```sql
SELECT * 
FROM scores 
ORDER BY score DESC 
LIMIT 20;
```
#### 🔹 Tutor Salary Assessment: Rounded average salary of all teachers
```sql
SELECT ROUND(AVG(teacher_salary), 2) AS avg_salary 
FROM teacher;
```

#### 🔹 List of courses and their respective departments
```sql
SELECT course_name, department 
FROM courses;
```
#### 🔹 Students scoring above 75 with their respective courses
```sql
SELECT student_name, course_id, score 
FROM scores 
WHERE score > 75;
```
#### 🔹 All courses, including those without assigned teachers
```sql
SELECT c.course_name, t.teacher_name 
FROM courses c 
LEFT JOIN teacher t ON c.teacher_id = t.teacher_id;
```
#### 🔹 List of all students with their respective courses (including those not assigned to any)
```sql
SELECT s.student_name, c.course_name 
FROM students s 
LEFT JOIN scores sc ON s.student_id = sc.student_id 
LEFT JOIN courses c ON sc.course_id = c.course_id;
```
#### 🔹 Courses with their total student enrollments (including courses with no students enrolled)
```sql
SELECT c.course_name, COUNT(s.student_id) AS total_students 
FROM courses c 
LEFT JOIN scores s ON c.course_id = s.course_id 
GROUP BY c.course_name;
```

#### 🔹 Teachers and their salaries in decimal format
```sql
SELECT teacher_name, CAST(teacher_salary AS DECIMAL(10,2)) AS salary 
FROM teacher;
```
#### 🔹 Teachers and their salaries displayed in dollars
```sql
SELECT teacher_name, CONCAT('$', FORMAT(teacher_salary, 2)) AS salary 
FROM teacher;
```
#### 🔹 Number of students scoring above the average score
```sql
WITH avg_score AS (
    SELECT AVG(score) AS overall_avg 
    FROM scores
)
SELECT COUNT(student_id) 
FROM scores 
WHERE score > (SELECT overall_avg FROM avg_score);
```
#### 🔹 Teachers with salaries below the average salary
```sql
SELECT teacher_name, teacher_salary 
FROM teacher 
WHERE teacher_salary < (SELECT AVG(teacher_salary) FROM teacher);
```

## 📌 Key Insights
- **Student Performance:** 40% of students scored above 70, with an average Advanced Excel score of 75.6.
- **Course Popularity:** The 'Data Science' department offers the most courses, while 'Blockchain' has the fewest.
- **Teacher Salary:** The average teacher salary is $55,000, with 20% earning below average.
- **Enrollment Gaps:** 10% of students are not enrolled in any courses, indicating potential registration issues.

## 🏆 Conclusion & Recommendations
- **Improve Student Support:** Extra tutoring for courses with an average score below 50.
- **Optimize Course Distribution:** Consider adding more courses to underrepresented departments.
- **Increase Teacher Salaries:** Adjust salaries for teachers earning below average to improve retention.
- **Enhance Student Enrollment:** Address missing enrollments to ensure all students actively learn.

---

## 💻 Technologies Used
- **Database:** PostgreSQL
- **Languages:** SQL

---

### 📢 Connect with Me on LinkedIn: [[Your LinkedIn](https://www.linkedin.com/in/tobiosinubi/)]  
