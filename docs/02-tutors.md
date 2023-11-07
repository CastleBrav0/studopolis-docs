# Tutor API Documentation

The Tutor API defines a set of endpoints that are accessible for authorized users. These endpoints are intended for users with the "tutor" role and require a valid JSON Web Token (JWT) to be included in the request headers for authentication. Below is an overview of the available endpoints and their functionalities.

## Authentication

In order to access any endpoint under `/tutor/`, a valid JWT must be present in the request headers. Example JWT in the `Authorization` header:

```
Authorization: eyJhbGciOiJFUzI1NiIsInR5cCI6IkpXVCJ9.eyJ...
```

## `/tutor/whoami` - Get Tutor Information

- **HTTP Method:** `GET`
- **Endpoint:** `/tutor/whoami`

This endpoint provides information about the currently authenticated tutor, including their user ID, email, and role.

- ### Example response:
    ```json
    {
      "id": "50174999-a1b8-471c-af5f-c7258b87af8b",
      "email": "tutor@mail.org",
      "role": "tutor"
    }
    ```

## `/tutor/create-course` - Create a New Course

- **HTTP Method:** `POST`
- **Endpoint:** `/tutor/create-course`

Create a new course with the specified title.

- ### Request Body
    ```json
    {
      "title": "My Course"  // Title of the course :string:
    }
    ```
- ### Response
    ```json
    {
      "id": "094303d7-2ed1-44dd-9a82-2623c911d361",         // Course ID
      "owner_id": "50174999-a1b8-471c-af5f-c7258b87af8b",   // Tutor's ID who onwes this course
      "title": "My Course",                                 // Course title
      "publish_date": "0001-01-01T00:00:00Z"                // Publish date (created automatically)
    }
    ```
## `/tutor/my` - Get Tutor's Courses

- **HTTP Method:** `GET`
- **Endpoint:** `/tutor/my`

Retrieve a list of courses associated with the authenticated tutor.

- ### Response Example
    ```json
    [
      {
        "id": "80db2ce1-1412-4b65-b759-62b294a94615",
        "owner_id": "50174999-a1b8-471c-af5f-c7258b87af8b",
        "title": "My First Course",
        "publish_date": "2023-11-05T00:42:38.724874Z"
      },
      {
        "id": "3a1fe138-dfa0-4f31-a70c-be926bc47138",
        "owner_id": "50174999-a1b8-471c-af5f-c7258b87af8b",
        "title": "My Second Course",
        "publish_date": "2023-11-05T00:42:43.715678Z"
      },
      {
        "id": "b3fe3bbc-2bc2-4530-9013-fcf30065751e",
        "owner_id": "50174999-a1b8-471c-af5f-c7258b87af8b",
        "title": "My 5 Course",
        "publish_date": "2023-11-05T15:14:43.84107Z"
      },
      {
        "id": "094303d7-2ed1-44dd-9a82-2623c911d361",
        "owner_id": "50174999-a1b8-471c-af5f-c7258b87af8b",
        "title": "My Course",
        "publish_date": "2023-11-05T22:52:21.716447Z"
      }
    ]
    ```

## `/tutor/course/{course_id}` - Course-specific Endpoints

The following endpoints are accessible under `/tutor/course/{course_id}`. These endpoints are used for managing specific courses and their lessons.

- **`/tutor/course/{course_id}` - Get Course Information**
  - **HTTP Method:** `GET`
  - This endpoint provides information about the course with the specified `course_id`.
  - ### Example
    - #### Request
        `GET <server>/tutor/course/80db2ce1-1412-4b65-b759-62b294a94615`
    - #### Response
        ```json
        {
          "id": "80db2ce1-1412-4b65-b759-62b294a94615",
          "owner_id": "50174999-a1b8-471c-af5f-c7258b87af8b",
          "title": "My First Course",
          "publish_date": "2023-11-05T00:42:38.724874Z"
        }
        ```

- **`/tutor/course/{course_id}/create-lesson` - Create a New Lesson**
  - **HTTP Method:** `POST`
  - Create a new lesson within the course specified by `course_id`.

    - #### Request Body
        ```json
        {
          "title": string,    // Title of the lesson
          "video": string     // Content of the lesson
        }
        ```
        At the moment server uploads local videos. Currently working upload mechanism will be shown in section `04-uploads`. The overall concept will be like described above. User provides only title, `"video":`  is (currently) only a technical field to serach for local videos and upload them. 

- **`/tutor/course/{course_id}/list-lessons` - List Lessons in a Course**
  - **HTTP Method:** `GET`
  - List all the lessons associated with the course specified by `course_id`.
  - ### Example
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

## Additional Information

- Make sure to include a valid JWT in the `Authorization` header when making requests to the `/tutor/` endpoints.
