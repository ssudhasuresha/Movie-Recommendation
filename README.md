# Movie-Recommendation

# Content-based recommendation system

Here, a movie recommender engine is developed that will create a profile of a user and then match 10 randomly selected movies to the user’s profile; the top 5 movies will be suggested to the user as possible movies to watch.


## Dataset
The MovieLens dataset is collected from the repository of the University of Minnesota (https://grouplens.org/datasets/movielens/). This dataset was generated on October 17, 2016. This dataset is available to program (see ml-latest-small.zip file). For this project, I have considered only two files in the dataset: ratings.csv and movies.csv. The file ratings.csv contains ratings of 671 users, each user is identified by a unique user ID. The file movies.csv contains movies, titles, and genres, each movie is identified by a unique movie ID. I have used only a small sample of the dataset that consists of 100004 ratings and 1296 tag applications across 9125 movies. 

## Packages
The project is implemented using the R language. The Isa package is used to calculate cosine similarity.

## Approach
The user id in the profile is created using 20417349 mod 671. Once the user's profile is created, then randomly choosing 10 movies from the movies.csv file. For example, if choose randomly 10 movies IDS: 1881, 7419, 4502, 1050, 5533, 92535, 4927, 6941, 505, 1371. The movie ID 1881 in the movies.csv file is Quest for Camelot (1998), 7419 is After Hours (1985), 4502 is Ernest Saves Christmas (1988), and so on. Then created a profile for each movie. Once the user's profile and movie profile is created, the program will use the cosine similarity metric to get the similarity between the user and each of the movies. After calculating the cosine similarity for each movie and user, the program will output the top 5 movies with the highest similarity that match the user’s profile.

# Implementation

## Building a User Profile
The program will examine all of the movies that the user has watched. (Watch out, one user in the dataset has matched 2391 movies if the program randomly picks that user then makes sure to test the code on a user who has watched fewer movies. For example, the least amount of movie watched is 20, and the user id is 1.) 

The profile will be constructed in 20 dimensions. Each genre of the movies that the user has watched becomes an attribute. Then will go through all of the movies that a user has watched and extract genres of the movies. The genres in the dataset are separated by '|'. The strsplit() function in the R language is used to extract genres.

These are the 20 genres that are present in the movies.csv file:

"Action", "Adventure", "Animation", "Children", "Comedy", "Crime", "Documentary", "Drama", "Fantasy", "Film-Noir", "Horror", "IMAX", "Musical", "Mystery", "Romance", "Sci-Fi", "Thriller", "War", "Western", "(no genres listed)".

The User's profile is created by creating a data frame with 20 columns and as many rows as the number of movies that the user has watched. Then each movie is decomposed into its constituent genres and the appropriate cells in the data frame corresponding to the genre are set to ‘1’. The user's profile is generated by summing up the 1's in each attribute and dividing them by the number of movies watched by that user.

## Building a Movie Profile
The movie profile is created by extracting all of the genres that the movie can be decomposed into and the column corresponding to the genre of the movie gets set to a ‘1’ and all other columns get set to ‘0’. For example, movie ID number 145 is decomposed into the following genres: “Action”, “Comedy”, “Crime”. “Drama”, “Thriller”. The movie vector corresponding to this movie will be: <1, 0, 0, 0, 1, 1, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0>. Here, the first element corresponds to genre "Action", the second "Adventure", and so on.

## Output
After creation of user's profile and movie profile, 5 movies are recommended using cosine similarity. The cosine similarity of the user profile vector and the movie profile vector shown above is: 0.666

The output generated as 

User ID  161 chose the following 10 movies: 18, 47, 255, 269, 471, 445, 640, 680, 1589, 1562
Of these, the following 5 movies are recommended:

		MovieId 	MovieName 	Similarity
		1562 		Title 1 	0.671
		445 		Title 2 	0.584
		680 		Title 3 	0.221
		471 		Title 4 	0.195
		255 		Title 3 	0.108
