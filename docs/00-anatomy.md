# API Documentation
Thats some sort of a documentation for studopolis wiki. More detailed look at the endpoints could be found in next pages.
## Database
Consists of 4 tables, before creating anything it is recommended to run 
```sql
DROP TABLE IF EXISTS student_courses, lessons, courses, users;
```
  - ### Table `users`
    ```sql
    CREATE TABLE users (
      id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
      email VARCHAR(255) NOT NULL UNIQUE,
      encrypted_password VARCHAR(255) NOT NULL,
      role VARCHAR(10) CHECK (role IN ('student', 'tutor')) DEFAULT   'student'
    );
    ```
  - ### Table `courses` 
    ```sql
    CREATE TABLE courses (
      id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
      owner_id UUID REFERENCES users(id),
      title varchar(100) NOT NULL,
      publish_date timestamp DEFAULT current_timestamp
    );
    ```
  - ### Table `lessons`
    ```sql
    CREATE TABLE lessons (
      id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
      title TEXT,
      course_id UUID REFERENCES courses(id),
      code TEXT,
      publish_date timestamp DEFAULT current_timestamp
    );
    ```
  - ### Table `student_courses`
    ```sql
    CREATE TABLE student_courses (
      student_course_id UUID PRIMARY KEY,
      student_id UUID REFERENCES users(id),
      course_id UUID REFERENCES courses(id),
      purchase_date DATE
    );
    ```
## Streamable
  Streamable is managed via backend. All it needs is `STRM_USERNAME` and `STRM_PWD` environmental variables.

## Server configs
  Server config is defined in `configs/apiserver.toml` and consists of 4 fields
  - **bind_addr**
  - **log_level**
  - **database_url** 
  - **session_key**

## JWE Config
  JWE Config is located in `configs/jwe.toml` and specifies path to `.pem` file.


```
          _____                    _____                    _____            _____                    _____                    _____                    _____          
         /\    \                  /\    \                  /\    \          /\    \                  /\    \                  /\    \                  /\    \         
        /::\____\                /::\    \                /::\____\        /::\____\                /::\    \                /::\    \                /::\    \        
       /::::|   |               /::::\    \              /:::/    /       /:::/    /               /::::\    \              /::::\    \              /::::\    \       
      /:::::|   |              /::::::\    \            /:::/    /       /:::/    /               /::::::\    \            /::::::\    \            /::::::\    \      
     /::::::|   |             /:::/\:::\    \          /:::/    /       /:::/    /               /:::/\:::\    \          /:::/\:::\    \          /:::/\:::\    \     
    /:::/|::|   |            /:::/__\:::\    \        /:::/    /       /:::/____/               /:::/__\:::\    \        /:::/__\:::\    \        /:::/__\:::\    \    
   /:::/ |::|   |           /::::\   \:::\    \      /:::/    /        |::|    |               /::::\   \:::\    \      /::::\   \:::\    \      /::::\   \:::\    \   
  /:::/  |::|___|______    /::::::\   \:::\    \    /:::/    /         |::|    |     _____    /::::::\   \:::\    \    /::::::\   \:::\    \    /::::::\   \:::\    \  
 /:::/   |::::::::\    \  /:::/\:::\   \:::\    \  /:::/    /          |::|    |    /\    \  /:::/\:::\   \:::\    \  /:::/\:::\   \:::\____\  /:::/\:::\   \:::\    \ 
/:::/    |:::::::::\____\/:::/  \:::\   \:::\____\/:::/____/           |::|    |   /::\____\/:::/__\:::\   \:::\____\/:::/  \:::\   \:::|    |/:::/__\:::\   \:::\____\
\::/    / ~~~~~/:::/    /\::/    \:::\  /:::/    /\:::\    \           |::|    |  /:::/    /\:::\   \:::\   \::/    /\::/   |::::\  /:::|____|\:::\   \:::\   \::/    /
 \/____/      /:::/    /  \/____/ \:::\/:::/    /  \:::\    \          |::|    | /:::/    /  \:::\   \:::\   \/____/  \/____|:::::\/:::/    /  \:::\   \:::\   \/____/ 
             /:::/    /            \::::::/    /    \:::\    \         |::|____|/:::/    /    \:::\   \:::\    \            |:::::::::/    /    \:::\   \:::\    \     
            /:::/    /              \::::/    /      \:::\    \        |:::::::::::/    /      \:::\   \:::\____\           |::|\::::/    /      \:::\   \:::\____\    
           /:::/    /               /:::/    /        \:::\    \       \::::::::::/____/        \:::\   \::/    /           |::| \::/____/        \:::\   \::/    /    
          /:::/    /               /:::/    /          \:::\    \       ~~~~~~~~~~               \:::\   \/____/            |::|  ~|               \:::\   \/____/     
         /:::/    /               /:::/    /            \:::\    \                                \:::\    \                |::|   |                \:::\    \         
        /:::/    /               /:::/    /              \:::\____\                                \:::\____\               \::|   |                 \:::\____\        
        \::/    /                \::/    /                \::/    /                                 \::/    /                \:|   |                  \::/    /        
         \/____/                  \/____/                  \/____/                                   \/____/                  \|___|                   \/____/         
                                                                                                                                                                       

```