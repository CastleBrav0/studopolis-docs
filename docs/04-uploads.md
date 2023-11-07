# Uploads

Now the interesting part. Currently they are in unfinished state, but current upload template will stay the same no matter the 

## The `right` way (prefered)
Send `POST` request to full endpoint.
The request itself is a `form` with specific fields:
- **title**: video title, basic `string`
- **file**: the attached file (could be practically anything, even .jpegs work)

### Example
- #### Headers
  ```
  Authorization: eyJhbGciOiJFUzI1NiIsInR5cCI6IkpXVCJ9.eyJhdWQiOlsidHV0b3IiXSwiZXhwIjoxNjk5ODcyOTE4LCJpYXQiOjE2OTkyNjgxMTgsImlzcyI6IlN0dWRvcG9saXMiLCJ1c2VyIjp7ImlkIjoiMjYxZjE3MDQtMzkzYi00MzJmLWJjNDAtMjM3ZTY1MjgxY2YwIiwiZW1haWwiOiJ0dXRvcjFAbWFpbC5vcmciLCJyb2xlIjoidHV0b3IifX0.4G3IXvzSpRYhKHKzrLz7cbe7I93OQVuHwU5LK5HIAQ4bQ0OgiBM9NUsC2Jpg0qWOnp2PQfSSdSS8ayFlYerDiw
  ```
- #### Request 
  
    ```
    POST https://studopolis-4p4r.onrender.com/tutor/course/6b6ea8eb-f1f9-4fcd-9c57-690822c70766/create-lesson
    ```
    **ATTACH FORM BODY WITH FILE!**
- #### Form Example
    ![form example](./pics/form-example.png)
- #### Response
    ```json
    {
      "id": "6194d1cf-6b3d-4ad3-a27a-4cf72cd2991a",
      "title": "My Second Lesson",
      "course_id": "6b6ea8eb-f1f9-4fcd-9c57-690822c70766",
      "code": "aa74o8",
      "publish_date": "0001-01-01T00:00:00Z"
    }
    ```

## The `easy` way
Just use `<server>/upload` endpoint

## Watching videos

### Example
- #### Headers
  Must be a valid `student` JWT, for example:
    ```
    Authorization: eyJhbGciOiJFUzI1NiIsInR5cCI6IkpXVCJ9.eyJhdWQiOlsic3R1ZGVudCJdLCJleHAiOjE2OTk4NzM2NzMsImlhdCI6MTY5OTI2ODg3MywiaXNzIjoiU3R1ZG9wb2xpcyIsInVzZXIiOnsiaWQiOiI3YjliYTc2MS02MTFiLTQzNGUtYmU5NS0xMTMwYzg0N2NmNjAiLCJlbWFpbCI6InN0dWRlbnRAbWFpbC5vcmciLCJyb2xlIjoic3R1ZGVudCJ9fQ.-mgYzH802h2FOUFR_dW8GOlKwIOzvrcUnzJYGn1I_OMYs4pR8Ty4JKUcGF3q2Nf0lcfRofkVoh6Es1TsllxlaQ
  ```

- #### Request 

  ```
  GET https://studopolis-4p4r.onrender.com/student/my/6b6ea8eb-f1f9-4fcd-9c57-690822c70766/p/c3de46d9-4914-4b58-bee6-a54ef835ac24
  ```

- #### Response
  HTML-embeded video
  ```html
  <div style="width:100%;height:0px;position:relative;padding-bottom:177.778%;">
  <iframe src="https://streamable.com/e/8dpdg6" frameborder="0" width="100%"
    height="100%" allowfullscreen
    style="width:100%;height:100%;position:absolute;left:0px;top:0px;overflow:hidden;"></iframe>
  </div>
  ```

  # Troubleshooting

  If this doc is more than 7-days-old, the JWT's will probably be expired, before accesing any endpoints, retrieve new ones with

  - ### Request
  ```
  POST https://studopolis-4p4r.onrender.com/login
  ```
  - ### Request body
  ```json
  {
    "email": "tutor@mail.org",
    "password": "password"
  }
  ```
  **OR**
  ```json
  {
    "email": "student@mail.org",
    "password": "password"
  }
  ```