# SignUp, Login, Authorization

## Signup Endpoint

The Signup endpoint allows users to create a new account. Users can sign up by providing their email, password, and role information in the request body. Upon successful registration, a new user account will be created.

- **HTTP Method:** `POST`
- **Endpoint:** `/signup`

### Request

The request to this endpoint should include the following JSON fields in the request body:

#### Request Body

```json
{
  "email": string,   // User's email address
  "password": string,  // User's password
  "role": string  // User's role (either "student" or "tutor")
}
```
### Examples
Creating `student` registry:
- Request:

    `POST <server>/signup`
    ```json
    {
      "email": "student2@mail.org",
      "password": "password"
    }
    ```
- Response:
    ```json
    {
      "id": "e5075cbf-ee27-43dd-8481-e4092bff661e",
      "email": "student2@mail.org",
      "role": "student"
    }
    ```
Creating `tutor` registry:

Just include `"role": "turor"` in JSON payload.
- Request:

    `POST <server>/signup`
    ```json
    {
      "email": "tutor.user@mail.org",
      "password": "password",
      "role": "tutor"
    }
    ```
- Response:
    ```json
    {
      "id": "66d3bae9-54c7-491e-87ee-b8e612253f3c",
      "email": "tutor.user@mail.org",
      "role": "tutor"
    }
    ```


## Login Endpoint

Login Endpoint searches user in DB, and if corresponding user is found -> JWT Auth (JSON Web Token) is generated. It contains encrypted user information (id and role), is signed and has deafult expire period of 7 days. In order to access protected endpoints, `Authorization` Header must be set.

- **HTTP Method:** `POST`
- **Endpoint:** `/login`

### Request

The request to this endpoint should include the following JSON fields in the request body:

#### Request Body

```json
{
  "email": string,   // User's email address
  "password": string  // User's password
}
```
### Examples
Authorizing a user:

Spicifying a role is not needed since it's already stored in DB and will be backed into JWT's claims.

- Request

    `POST <server>/login`
    ```json
    {
      "email": "tutor.user@mail.org",
      "password": "password"
    }
    ```
- Response
    ```
    eyJhbGciOiJFUzI1NiIsInR5cCI6IkpXVCJ9.eyJhdWQiOlsidHV0b3IiXSwiZXhwIjoxNjk5ODE3MzE3LCJpYXQiOjE2OTkyMTI1MTcsImlzcyI6IlN0dWRvcG9saXMiLCJ1c2VyIjp7ImlkIjoiNjZkM2JhZTktNTRjNy00OTFlLTg3ZWUtYjhlNjEyMjUzZjNjIiwiZW1haWwiOiJ0dXRvci51c2VyQG1haWwub3JnIiwicm9sZSI6InR1dG9yIn19.jmO5rnDlDOWSaBmndCtLOdY_gZl3lob0SIESZLOKKA8eZPYPhTUqyPsGimhOHmv1oWpqhR5gcuDGCvvRg6X1fw
    ```

## Authorizing
When JWT is acquiried, it must be specified in Headers in order to gain access to protected endpoints (`/student/..`, `/tutor/..`, etc.)

### Headers Example:

Practically the import thing is only the `Authorization` header, everything else could be anything, including `nill`
```
Accept: */*
User-Agent: Mozilla/5.0 (Linux; Linux i541 ; en-US) Gecko/20100101 Firefox/72.1
Authorization: eyJhbGciOiJFUzI1NiIsInR5cCI6IkpXVCJ9.eyJhdWQiOlsidHV0b3IiXSwiZXhwIjoxNjk5ODE3MzE3LCJpYXQiOjE2OTkyMTI1MTcsImlzcyI6IlN0dWRvcG9saXMiLCJ1c2VyIjp7ImlkIjoiNjZkM2JhZTktNTRjNy00OTFlLTg3ZWUtYjhlNjEyMjUzZjNjIiwiZW1haWwiOiJ0dXRvci51c2VyQG1haWwub3JnIiwicm9sZSI6InR1dG9yIn19.jmO5rnDlDOWSaBmndCtLOdY_gZl3lob0SIESZLOKKA8eZPYPhTUqyPsGimhOHmv1oWpqhR5gcuDGCvvRg6X1fw
```