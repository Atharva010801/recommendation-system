# recommendation-system
import numpy as np

# Sample movie ratings matrix (rows: users, columns: movies)
# Replace this with your own data or use a dataset like MovieLens.
ratings = np.array([
    [5, 4, 0, 0, 1],
    [0, 0, 5, 4, 2],
    [3, 0, 0, 0, 4],
    [0, 3, 4, 0, 5],
])

def recommend_movies(ratings, user_id, num_recommendations=5):
    user_ratings = ratings[user_id]
    unrated_movies = np.where(user_ratings == 0)[0]

    if len(unrated_movies) == 0:
        print("You've rated all movies.")
        return

    movie_scores = np.sum(ratings[:, unrated_movies], axis=0)
    top_movies = np.argsort(movie_scores)[::-1][:num_recommendations]

    print("Recommended movies:")
    for i, movie_id in enumerate(top_movies):
        print(f"{i+1}. Movie {movie_id + 1} (Score: {movie_scores[movie_id]})")

if __name__ == "__main__":
    user_id = int(input("Enter user ID (0 to 3): "))
    recommend_movies(ratings, user_id)
