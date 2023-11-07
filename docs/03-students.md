# Student API Documentation

The Student API defines a set of endpoints that are accessible for authorized users with the `"student"` role. These endpoints require a valid JSON Web Token (JWT) to be included in the request headers for authentication. Below is an overview of the available endpoints and their functionalities.

## Authentication

In order to access any endpoint under `/student/`, a valid JWT must be present in the request headers. Example JWT in the `Authorization` header:

```
Authorization: eyJhbGciOiJFUzI1NiIsInR5cCI6IkpXVCJ9.eyJ...
```

## `/student/` - Get Student Information

- **HTTP Method:** GET
- **Endpoint:** `/student/`

This endpoint provides information about the currently authenticated student, including their user ID, email, and role.

- ### Response Body 
  ```json
  {
    "id": "7b9ba761-611b-434e-be95-1130c847cf60",
    "email": "student@mail.org",
    "role": "student"
  }
  ```

## `/student/buy` - Buy a Course

- **HTTP Method:** POST
- **Endpoint:** `/student/buy`

Buy a course with the specified `course_id`.



- ### Request Body
  ```json
  {
    "course_id": string  // ID of the course to be purchased
  }
  ```
  This creates a special relation in `student_courses` table which specifies many-to-many relation between students and courses they bought
  
- ### Response Body 
  ```json
  {
    "student_course_id": "4ddca7bb-edc4-4e60-9230-7bf6eba24bd6",
    "student_id": "7b9ba761-611b-434e-be95-1130c847cf60",
    "course_id": "6b6ea8eb-f1f9-4fcd-9c57-690822c70766",
    "purchase_date": "2023-11-06T11:09:55.395391744Z"
  }
  ```

## `/student/my` - Get Student's Courses

- **HTTP Method:** GET
- **Endpoint:** `/student/my`

    - ### Response Example
        ```json
        [
          {
            "student_course_id": "4f7713e5-fb8a-4751-8323-83430180152a",    // Relation ID
            "student_id": "975b680e-a412-4b1a-b361-cba39031b808",           // Student ID
            "course_id": "3a1fe138-dfa0-4f31-a70c-be926bc47138",            // ID of a Course thta student above ownes
            "purchase_date": "2023-11-05T00:00:00Z"                         // Realtion creation date
          },
          {
            "student_course_id": "43df0b9e-a5e2-4711-9ac1-503ffb786b27",
            "student_id": "975b680e-a412-4b1a-b361-cba39031b808",
            "course_id": "80db2ce1-1412-4b65-b759-62b294a94615",
            "purchase_date": "2023-11-05T00:00:00Z"
          }
        ]
        ```

Retrieve a list of courses associated with the authenticated student.

## `/student/my/{course_id}` - Course-specific Endpoints

The following endpoints are accessible under `/student/my/{course_id}`. These endpoints are used for accessing specific courses and their lessons.

- **`/student/my/{course_id}` - Get Course Lessons**
  - **HTTP Method:** GET
  - This endpoint provides a list of lessons associated with the course specified by `course_id`.
  - ### Example 
    - #### Request
        `GET <server>/student/my/80db2ce1-1412-4b65-b759-62b294a94615`
    - #### Response Body
        ```json
        [
          {
            "id": "44d87f02-7eba-4736-ae81-6c09e95fe94a",
            "title": "My First Lesson",
            "course_id": "80db2ce1-1412-4b65-b759-62b294a94615",
            "code": "65shc1",
            "publish_date": "2023-11-05T01:58:01.979832Z"
          },
          {
            "id": "9b3052e0-b9a7-4993-b186-fcc11742d8a5",
            "title": "My First Lesson",
            "course_id": "80db2ce1-1412-4b65-b759-62b294a94615",
            "code": "3jz5b8",
            "publish_date": "2023-11-05T01:58:08.228412Z"
          },
          {
            "id": "0cd1a9d4-27aa-45f0-b1d8-8a7bbdf21d18",
            "title": "My Third Lesson",
            "course_id": "80db2ce1-1412-4b65-b759-62b294a94615",
            "code": "c70uyw",
            "publish_date": "2023-11-05T01:58:22.355585Z"
          }
        ]
        ```

## `/student/my/{course_id}/p/{lesson_id}` - Play Video

- **HTTP Method:** GET
- **Endpoint:** `/student/my/{course_id}/p/{lesson_id}`

This endpoint allows students to play a video lesson. The video is embedded using the following HTML code:

```html
<div style="width:100%;height:0px;position:relative;padding-bottom:177.778%;">
    <iframe src="https://streamable.com/e/{{video_id}}" frameborder="0" width="100%" height="100%" allowfullscreen style="width:100%;height:100%;position:absolute;left:0px;top:0px;overflow:hidden;"></iframe>
</div>
```
- ### Example Request
    `GET <server>/student/my/80db2ce1-1412-4b65-b759-62b294a94615/p/44d87f02-7eba-4736-ae81-6c09e95fe94a`


## Additional Information

- Ensure that a valid JWT is included in the `Authorization` header for authentication.
