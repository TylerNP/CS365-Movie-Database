### Example Flows

John Smith just watched a new movie in the theatres. He really enjoyed this movie and would like to see similar movies. He goes on (our project) and searches for the movie he just watched. He adds it to his list of liked movies and rates it from 1-10. John then requests to see movies like the one he just likes and rated.

John starts by logging into or signing up for an account 
He calls SEARCH and inputs the movie he just watched.
He calls ADD to his liked movie list with his rating.
He decides he would like to see which movies are similar to the movie he just watched so he calls RECOMMEND

#### Advanced search feature
Jane, a user who wants to see a movie but doesn’t know the movie title, wants to search for the movie using the director(which she knows).

She first signs up with a POST request to `/users/signup`. She then searches for the director’s movies with a GET request to `/attributes/:director`. She then looks at one she likes with a GET request to /`movies/:id`.
She now has all the info she needs to watch the movie.

