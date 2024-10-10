# CSC365 Movie Databases 

# Taran
3) As a user I want to rate movies as I like them or don’t like them, so that i can get recommendations of what other movies I might like   (rate movies)

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
