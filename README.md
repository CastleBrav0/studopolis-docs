```
   ▄████████     ███     ███    █▄  ████████▄   ▄██████▄     ▄███████▄  ▄██████▄   ▄█        ▄█     ▄████████ 
  ███    ███ ▀█████████▄ ███    ███ ███   ▀███ ███    ███   ███    ███ ███    ███ ███       ███    ███    ███ 
  ███    █▀     ▀███▀▀██ ███    ███ ███    ███ ███    ███   ███    ███ ███    ███ ███       ███▌   ███    █▀  
  ███            ███   ▀ ███    ███ ███    ███ ███    ███   ███    ███ ███    ███ ███       ███▌   ███        
▀███████████     ███     ███    ███ ███    ███ ███    ███ ▀█████████▀  ███    ███ ███       ███▌ ▀███████████ 
         ███     ███     ███    ███ ███    ███ ███    ███   ███        ███    ███ ███       ███           ███ 
   ▄█    ███     ███     ███    ███ ███   ▄███ ███    ███   ███        ███    ███ ███▌    ▄ ███     ▄█    ███ 
 ▄████████▀     ▄████▀   ████████▀  ████████▀   ▀██████▀   ▄████▀       ▀██████▀  █████▄▄██ █▀    ▄████████▀  
                                                                                  ▀                           

```

# Server Endpoints

## **Detailed Docs could be found [HERE](/docs/)**

This README provides an overview of the endpoints and their functionality in the `server`.



## Table of Contents
- [Request Logging and CORS Headers](#request-logging-and-cors-headers)
- [User Authentication](#user-authentication)
- [Student Endpoints](#student-endpoints)
  - [Retrieve User Information](#retrieve-user-information)
  - [Buy a Course](#buy-a-course)
  - [List Student Courses](#list-student-courses)
  - [Student Course Details](#student-course-details)
    - [List Course Lessons](#list-course-lessons)
    - [Play Video Lessons](#play-video-lessons)
- [Tutor Endpoints](#tutor-endpoints)
  - [Retrieve User Information](#retrieve-user-information-1)
  - [Create a Course](#create-a-course)
  - [List User Courses](#list-user-courses)
  - [Course Details](#course-details)
    - [Create a Lesson](#create-a-lesson)
    - [List Course Lessons](#list-course-lessons-1)

### Request Logging and CORS Headers
- `GET /signup`: Creates a user in the database.
- `POST /login`: Checks if a user exists in the database.
- `GET /proxy`: Proxies traffic over the server's endpoint.
- `GET /upload`: Retrieves Upload form from server
- ```html
  <form action="/upload" method="post" enctype="multipart/form-data">
        <input type="file" name="file">
        <input type="submit" value="Upload">
  </form>
  ```

### User Authentication
- Must provide Auth-Header. Example:
    ```
    Authorization: eyJhbGciOiJFUzI1NiIsInR5cCI6IkpXVCJ9.eyJhdWQiOlsic3R1ZGVudCJdLCJleHAiOjE2OTk3ODQxOTQsImlhdCI6MTY5OTE3OTM5NCwiaXNzIjoiU3R1ZG9wb2xpcyIsInVzZXIiOnsiaWQiOiI5NzViNjgwZS1hNDEyLTRiMWEtYjM2MS1jYmEzOTAzMWI4MDgiLCJlbWFpbCI6InN0dWRlbnRAbWFpbC5vcmciLCJyb2xlIjoic3R1ZGVudCJ9fQ.CnwbsVhbcEIPazdQq_KpzNaYcEIw8YEx5qpa_1szpbbWbNIznOV9LIvJXDRUGRCA712KM1EFqOsWI4H9TlBjQw
    ```

### Student Endpoints

#### Retrieve User Information
- `GET /student`: Retrieve information about the authenticated user.

#### Buy a Course
- `POST /student/buy`: Purchase a course.

#### List Student Courses
- `GET /student/my`: List courses available to the student.

#### Student Course Details
- `GET /student/my/{course_id}`: Retrieve details about a specific course.
  - `GET /student/my/{course_id}/p/{lesson_id}`: Play video lessons for a specific course and lesson.

### Tutor Endpoints

#### Retrieve User Information
- `GET /tutor`: Retrieve information about the authenticated tutor.

#### Create a Course
- `POST /tutor/create-course`: Create a new course.

#### List User Courses
- `GET /tutor/my`: List courses created by the tutor.

#### Course Details
- `GET /tutor/course/{course_id}`: Retrieve details about a specific course.
  - `POST /tutor/course/{course_id}/create-lesson`: Create a new lesson for the course.
  - `GET /tutor/course/{course_id}/list-lessons`: List lessons for the course.

Please note that certain endpoints require user authentication and specific permissions to access. Ensure that your application handles authentication and authorization appropriately.

For more detailed information on each endpoint's implementation, refer to the source code in the `server` package.