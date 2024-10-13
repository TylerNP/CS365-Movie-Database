# CSC365 Movie Databases 
### API Specification

## Users
### `/users/signup` (POST)
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
### `/users/login` (POST)
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
  "id": "integer"
}
```

### `/users/{id}/list/` (GET)
Retrieves user's list of movies <br />

**Request**:

```json
{
  "user_id": "integer" 
}
```
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

### `/users/{id}/list/{movie_id}/rate/}` (POST)
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

### `/users/{id}/list/{movie_id}/watched` (POST)
Log a movie as watched . <br />

**Response**:

```json
{
  "success": "boolean"
}
```

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
### Get Catalog - `/catalog` (GET)
Retrieves the catalog of movies. Each movie will only have one unique entry. <br />

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

### New Entry - `/catalog/movies` (POST)
Creates a new movie entry <br />

**Request**:

```json
{
        "name": "string",
        "director": "string",
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

## Recommendations
### Get Recommendations - `/recommend/{user_id}` (GET)
Creates a reocmmendation list based off user prefences (likes/dislikes) <br />

**Request**:

```json
{
        "user_id": "integer"
}
```
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

### Reset Recommendations - `/recommend/{user_id}/reset` (POST)
Reset a given users recommendations defaulting to most popular <br />

**Request**:

```json
{
        "user_id": "integer"
}
```

**Response**:
```json
{
        "success": "boolean"
}
```

### Delete Recommendation - `/recommend/{user_id}/delete/{movie_id}` (POST)
Removes a specific movie from the recommendation list of a user <br />

**Request**:

```json
{
        "user_id": "integer",
        "movie_id": "integer"
}
```

**Response**:

```json
{
        "success": "boolean"
}
```

### Generate Recommendation - `/recommend/{user_id}/generate` (POST)
Finds more movies to recommend to a user <br />

**Request**:

```json
{
        "user_id": "integer"
}
```

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



# Endpoints
1. Movies
1.1 Get Movie Info (generic info)
1.1. Get Random Movie


2. Users
2.1 Rate user



<<<<<<< HEAD
# 3 stories 

# Taran
3) As a user I want to rate movies as I like them or don’t like them, so that i can get recommendations of what other movies I might like   (rate movies)

=======
5) “As a user of (name of our project), I want to determine which upcoming movies will do well based on the movies I’ve liked. I’m a college student so time and money are limited and I’d want to pick the best possible choice.” (give rec. based on liked and not liked movies)
GET collabs /recommend/collabs

    Provides a list of movies that both an actor and director have worked on together. The call passes in two strings, the actor name and director name. Returns a list of movies that actor director has worked on together

Request: 
    [
        {
            'director' = 'string'
            'actors' = 'string'
        }
    ]

Respose:  a list of movie collabs between an actor and director
    [
        {
            'movie' = 'string'
        }
    ]
>>>>>>> e212bfdc49d151c0f1684bf10abfb2192b16460b



### Generate Recommendation based on collaborations - `/recommend/{user_id}/collab` (POST)
Provides a list of movies that both an actor and director have worked on together. The call passes in two strings, the actor name and director name. Returns a list of movies that actor director has worked on together <br />

**Request**:

```json
{
        "user_id": "integer",
        "actor" : "string",
        "director" : "string"
}
```

**Response**:

```json
[
    {
        "movie_id": "integer",
        "name": "string",
        "director": "string",
        "actor" : "string",
        "release_year": "integer",
        "genres": ["string"],  
        "average_rating": "integer"
    }
]
```



### GET analytics  - `/recommend/{user_id}/analytics` (POST)
Based on input, provides a list of movies that are doing well and what their budget - earnings are, audience rating, critic rating and demographic 
 <br />

**Request**:

```json
{
        "user_id": "integer",
        "genre": "string",
        
}
```

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


### GET availability  - `/recommend/{user_id}/availability` (POST)
Gives a list of movies that are available in certain subscription services or if free on line
 <br />

**Request**:

```json
{
        "user_id": "integer",
        "subscription": "string",
        
}
```

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




1. Get Random Movie Endpoint 
2. Post Rate Movie (0-10) (weight above a 5 is yes, below is no) # log movie into it 