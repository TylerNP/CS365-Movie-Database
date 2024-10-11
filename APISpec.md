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


7) “I am a film producer, and (name of our project) allows me to see which movie genres are doing well. They provide the metrics by user rating, critic reception, and budget to box-office earnings. This helps me to see which projects to invest in next.” (get movie data (analytics))

GET analytics  

    based on input, provides a list of movies that are doing well and what their budget - earnings are, audience rating, critic rating and demographic 

Request:
    [
        'genre' = 'string'
    ]

Response: 
    [
        'analysis' = 'string' #movies in this genre are doing well. they have net (this much millions) and their
        target demo are (this group of people).
    ]


9) As a movie enjoyer on a budget, I want to filter by free to watch movies (return movies that have sources that are free) (or if I have netflix, I want it to show me movies that are on netflix)

GET AVAILABILITY 

    gives a list of movies that are available in certain subscription services or if free on line

Request: 
    [
        {
            'subscription' = 'string' #netflix, hulu, youtube, free
        }
    ]

Response:
    [
        {
            'movies' = 'title' #list of movies that are available in those request
        }
    ]
1. Get Random Movie Endpoint 
2. Post Rate Movie (0-10) (weight above a 5 is yes, below is no) # log movie into it


