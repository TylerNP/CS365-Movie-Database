# CSC365 Movie Databases 
### API Specification

## Movies
### 1.1 Get Movie Info - `/movies/{movie_id}` (GET)
Obtain movie information. <br />

**Response**:

```json
{
      "movie_id": "integer",
      "name": "string",
      "director": "string",
      "actors": ["string"], /*List of actors in major roles*/
      "release_year": "integer",
      "genres": ["string"],  /*genres list size is capped at 6*/ 
      "average_rating": "integer"
}
```

### 1.2 New Entry - `/movies/new/` (POST)
Creates a new movie entry <br />

**Request**:

```json
{
      "movie_id": "integer",
      "name": "string",
      "director": "string",
      "actors": ["string"], /*List of actors in major roles*/
      "release_year": "integer",
      "genres": ["string"],  /*genres list size is capped at 6*/ 
      "average_rating": "integer"
}
```

**Response**:

```json
{
  "movie_id": "integer"
}
```

### 1.3 Get Movie Availabile - `/movies/availabile` (GET)
Gives a list of movies that are available with a certain subscription services or if free online <br />

**Request**:

```json
{
        "subscription": "string",
        
}
```

**Response**:

```json
[
    {
        "movie_id": "integer",
    }
]
```

## Users
### 2.1 User Signup - `/users/signup` (POST)
Create new user. <br />

**Request**:

```json
{
  "name": "string",
  "password": "string" 
}
```
**Response**:

```json
{
  "id": "integer"
}
```

### 2.2 User Login - `/users/login/{user_id}` (PUT)
Login existing user. <br />

**Request**:

```json
{
  "name": "string",
  "password": "string"
}
```
**Response**:

```json
{
  "user_id": "integer"
}
```

### 2.3 User List `/users/{id}/list/` (GET)
Retrieves user's list of movies <br />

**Response**:

```json
[
    {
        "movie_id": "integer"
    }
]
```

### 2.4 Rate Movie - `/users/{id}/rate/{movie_id}/` (POST)
Rate a movie. <br />

**Request**:

```json
{
  "rating": "integer" /*rating from 0 to 10*/
}
```
**Response**:

```json
{
  "success": "boolean"
}
```

### 2.5 Watched Movie - `/users/{id}/watched/{movie_id}` (POST)
Log a movie as watched or not. <br />

**Request**:

```json
{
  "watched": "boolean"
}
```
**Response**:

```json
{
  "success": "boolean"
}
```

==========================================
SHOULD GET CHANGED/MOVED DOESNT FIT PURPOSE OF USERS
### `/users/{id}/watch` (GET)
Get movies you haven't watched yet but have shown intrest in <br />

**Response**:

```json
[
    {
        "movie_id": "integer",
        "name": "string",
        "director": "string",
        "release_year": "integer",
        "genres": ["string"],  /*genres list size is capped at 6*/ 
        "average_rating": "integer"
    }
]
```

## Catalog
### 3.1 Get Catalog - `/catalog` (GET)
Retrieves the catalog of movies. Each movie will only have one unique entry. <br />

**Response**:

```json
[
    {
        "movie_id": "integer"
    }
]
```

### 3.2 Find Specific Movies - `/catalog/search, tags=["SEARCH"]` (GET)
Searches for movies based off querry parameters <br />

**Querry Parameters**:

- `movie_name`(optional): The name of the movie
- `genre`(optional): The genre of the movie
- `director`(optional): The director of the movie
- `actor`(optional): The actors in the movie
- `year`(optional): The release year of the movie
- `rating`(optional): The average rating of the movie
- `search_page`(optional): The page number of the results
- `sort_col`(optional): The column to sort the movies by. Possible values: `movie_name`, `genre`, `director`, `actor`, `year`, and `rating`
- `sort_order`(optional): The order the result appears. Possible values: `asc`(ascending) or `desc`(descending). Default: `asc`

**Response**:

The API responds with a JSON object with the following:
- `previous`: A string that represents the link to the previous search page if it exists. If no such page exists this string will be empty.
- `next`: A string that represents the link to the search next page if it exists. If no such page exists this string will be empty. 
- `results`: An array of objects, each representing a movie item. Each movie item has the following properties:
  - `movie_id`: An integer that represents the unique identifier of the movie item
  - `movie_name`: A string that holds the movie name
  - `movie_director`: A string that holds the director of the movie
  - `movie_release_year`: An integer holding the year of release of the movie
  - `movie_genres`: An array of strings storing the genres of the movie
  - `movie_average_rating`: An integer holding the average rating of the movie

## Recommendations
### 4.1 Get Recommendations - `/recommend/{user_id}` (GET)
Creates a reocmmendation list based off user prefences (likes/dislikes) <br />

**Response**:

```json
[
    {
        "movie_id": "integer"
    }
]
```

### 4.2 Reset Recommendations - `/recommend/{user_id}/reset` (POST)
Reset a given users recommendations defaulting to most popular <br />

**Response**:
```json
{
        "success": "boolean"
}
```

### 4.3 Delete Recommendation - `/recommend/{user_id}/delete/{movie_id}` (POST)
Removes a specific movie from the recommendation list of a user <br />

**Response**:

```json
{
        "success": "boolean"
}
```

### 4.4 Generate Recommendation - `/recommend/{user_id}/generate` (POST)
Finds more movies to recommend to a user <br />

**Response**:

```json
[
    {
        "movie_id": "integer"
    }
]
```

### 4.5 Generate Recommendation based on collaborations - `/recommend/{user_id}/collab` (POST)
Provides a list of movies that both an actor and director have worked on together. The call passes in two strings, the actor name and director name. Returns a list of movies that actor director has worked on together <br />

**Request**:

```json
{
        "actor" : "string",
        "director" : "string"
}
```

**Response**:

```json
[
    {
        "movie_id": "integer"
    }
]
```

## ANALYTICS
### 5.1 Get Analytics - `/analytics/{movie_id}` (GET)
Get the performance data of a movie <br />

**Response**:

```json
[
    {
        "movie_id": "integer",
        "name": "string",
        "director": "string",
        "release_year": "integer",
        "genres": ["string"],  
        "average_rating": "integer",
        "budget": "integer",
        "box-office": "integer",
        "demographic": "string"
    }
]
```

### 5.2 Get Analytics Genre - `/analytics/{genre}` (GET)
Based on genre, provides a list of movies that are doing well and what their budget - earnings are, audience rating, critic rating and demographic <br />

**Response**:

```json
[
    {
        "movie_id": "integer",
        "name": "string",
        "director": "string",
        "release_year": "integer",
        "genres": ["string"],  
        "average_rating": "integer",
        "budget": "integer",
        "box-office": "integer",
        "demographic": "string"
    }
]
```

## 5.3 Get Analytics Popular - `/analytics/popular` (GET)
Provides a list of the highest performing movies with respect to user reviews and box-office performance <br />

**Response**:

```json
[
    {
        "movie_id": "integer",
        "name": "string",
        "director": "string",
        "release_year": "integer",
        "genres": ["string"],  
        "average_rating": "integer",
        "budget": "integer",
        "box-office": "integer",
        "demographic": "string"
    }
]
```

### 5.4 Search Analytics - `/analytics/search, tag=["SEARCH"]`
Searches for movies based off querry parameters <br />

**Querry Parameters**:

- `movie_name`(optional): The name of the movie
- `budget`(optional): The budget of the movie
- `box-office`(optional): The box-office performance of the movie
- `demographic`(optional): The viewing demographic of the movie
- `sort_col`(optional): The column to sort the movies by. Possible values: `budget`, `box-office`, `demographic`, and `movie_name`
- `sort_order`(optional): The order the result appears. Possible values: `asc`(ascending) or `desc`(descending). Default: `asc`

**Response**:

The API responds with a JSON object with the following:
- `previous`: A string that represents the link to the previous search page if it exists. If no such page exists this string will be empty.
- `next`: A string that represents the link to the search next page if it exists. If no such page exists this string will be empty. 
- `results`: An array of objects, each representing an analytics item. Each analytics item has the following properties:
  - `movie_id`: An integer that represents the unique identifier of the movie item
  - `budget`: An integer representing the budget of the movie
  - `box-office`: An integer representing the performance of the movie in the box-office
  - `demographic`: A string that represents the demographics viewing the movie

## PREDICTIONS
### 6.1 Get Prediction - `/prediction/{movie_id}`
Attempts to predict the movie performance in the box-office and with specific demographics. <br />

**Response**:

```json
[
    {
        "predicted_rating": "integer",
        "box-office": "integer",
        "viewing_demographics": ["string"]
    }
]
```

## GROUP
### 7.1 Create Group - `/groups/{group_id}` (PUT)
Create a new group for users to join. <br />

**Request**:

```json
[
    {
        "group_name": "string",
        "group_desciprtion": "string",
        "group_interests": ["string"]
    }
]
```

**Response**:

```json

{
    "group_id": "integer" /*Unique number that identify a group*/
}

```

## ADMIN



1. Get Random Movie Endpoint 
2. Post Rate Movie (0-10) (weight above a 5 is yes, below is no) # log movie into it 




# Scratch Work 
## Endpoints
1. Movies
1.1 Get Movie Info (generic info)
1.1. Get Random Movie

2. Users
2.1 Rate user

3. Catalog

4. Recommend

5. 

6. Analytics

7. Group

8. Admin