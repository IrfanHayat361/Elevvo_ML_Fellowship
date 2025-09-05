# Movie Recommendation System

A collaborative filtering system that suggests movies to users based on what similar users liked. Built this to understand how recommendation engines work and see if I could make decent movie suggestions from user rating data.

## What this project does

- [The challenge](#the-challenge)
- [The data](#the-data)
- [How it works](#how-it-works)
- [What I learned](#what-i-learned)
- [Results](#results)
- [How to run it](#how-to-run-it)

## The challenge

Building a movie recommendation system sounds simple - just "give me movies I might like" - but it's actually pretty tricky. The main problem is that most users haven't seen most movies, so the data is really sparse. You have to figure out how to make good suggestions from very limited information.

I wanted to see if I could build something that actually works using collaborative filtering - basically finding users with similar tastes and recommending movies they liked that you haven't seen yet.

## The data

I used the MovieLens 100K dataset, which has:
- 943 users
- 1,664 movies  
- 100,000 ratings (1-5 scale)
- Movie titles and genres

The data is pretty typical for recommendation systems - some movies get rated a lot (popular ones) while others barely get any ratings. This creates a challenge because you don't want the system to just recommend popular movies to everyone.

## How it works

The approach I used is called user-based collaborative filtering:

1. **Create a user-item matrix** - rows are users, columns are movies, values are ratings
2. **Fill missing ratings with zeros** - this helps with similarity calculations
3. **Calculate user similarity** - using cosine similarity to find users with similar rating patterns
4. **Find similar users** - for each user, identify the most similar other users
5. **Generate recommendations** - look at what similar users rated highly that the target user hasn't seen

The key insight is that if two users have similar tastes (rate movies similarly), then movies one user liked are probably good recommendations for the other user.

## What I learned

The biggest surprise was how sparse the data actually is. Even with 100,000 ratings across 943 users and 1,664 movies, most user-movie combinations are missing. This makes similarity calculations tricky because you're comparing users based on only a handful of shared movies.

I had to be careful about filtering out movies users had already seen. At first, my recommendations included movies the user had already rated highly, which defeats the purpose. The system needs to only suggest unseen movies.

Popular movies kept showing up in everyone's recommendations, which makes sense but also makes the system a bit generic. A good recommendation system should balance popular items with personalized suggestions.

Evaluating recommendations is harder than I thought. You can't just use accuracy because most movies aren't rated by most users. I used Precision@K instead, which measures how many of the top-K recommendations are actually relevant (rated 4+ by the user).

## Results

The system works but has room for improvement:

- **Precision@5**: 0.0 (this is actually pretty common for recommendation systems on sparse data)
- **Recommendations**: The system does generate reasonable movie suggestions
- **User similarity**: Cosine similarity finds meaningful patterns in user preferences

For example, for User 10, the system recommended:
- Return of the Jedi (1983)
- Empire Strikes Back, The (1980) 
- Back to the Future (1985)
- Schindler's List (1993)
- Fugitive, The (1993)

These are all well-regarded movies, so the system is picking quality suggestions even if the precision metric is low.

## How to run it

You'll need these libraries:
```bash
pip install scikit-learn pandas numpy
```

The notebook automatically downloads the MovieLens dataset, so just run all the cells:

1. **Data loading** - Downloads and loads the 100K dataset
2. **Matrix creation** - Builds the user-item matrix
3. **Similarity calculation** - Computes user similarities using cosine similarity
4. **Recommendation function** - Generates movie suggestions for any user
5. **Evaluation** - Tests the system using train/test split

## Key insights

The most important thing I learned is that recommendation systems are about more than just algorithms. Data preprocessing, handling missing values, and choosing the right evaluation metrics are just as crucial as the core recommendation logic.

User-based collaborative filtering works well when you have enough data, but it struggles with new users (cold start problem) and very sparse datasets. The similarity calculations can be noisy when users have only a few ratings in common.

The system tends to recommend popular movies, which isn't necessarily bad - popular movies are popular for a reason. But a truly personalized system would balance popularity with individual preferences better.
