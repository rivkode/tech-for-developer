# ERD


간단한 과제를 통해 ERD 작성을 진행해보도록 합니다.

**과제 내용**

간단한 학사관리 시스템을 구축

**관계**

학과와 학생은 1 대 다 관계
- 학과는 많은 학생을 가질 수 있다.
- 학생은 한 학과에 소속된다.

학과와 교수는 1 대 다 관계
- 학과는 많은 교수를 가질 수 있다.
- 교수는 한 학과에 소속된다.

교수와 개설과목은 1 대 다 관계
- 교수는 많은 과목을 가르칠 수 있다.
- 과목은 강의하는 교수 한 명이 지정된다.

과목과 학생은 다 대 다 관계
- 과목은 수강하는 많은 학생을 가진다.
- 학생은 많은 과목을 수강할 수 있다.

**엔티티**

학생(Student)
- 학번(student_id), 성명(student_name), 키(height), `학과코드(department_id)`

학과(Department)
- 학과코드(department_id), 학과명(department_name)

교수(Professor)
- 교수코드(professor_id), 교수명(professor_name), `학과코드(department_id)`

개설과목(Course)
- 과목코드(course_id), 과목명(course_name), `교수코드(professor_id)`, 시작일(start_date), 종료일(end_date)

수강(Student_Course)
- `학번(student_id)`, `과목코드(course_id)`

> `외부참조 키(FK)` : 해당 엔티티와 관련된 데이터를 갖고 있는 프로터디가 아닌 다른 엔티티와의 관계를 설정하기 위한 키

<br>

<br>

<br>

![](https://user-images.githubusercontent.com/109144975/218555476-4d96a970-47f6-45de-b796-0a15475ef4e9.png)
