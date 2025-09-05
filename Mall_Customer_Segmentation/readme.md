# Mall Customer Segmentation

A clustering project that groups mall customers based on their income and spending patterns. I wanted to see if there were natural customer segments that could help with targeted marketing strategies.

## What this project does

- [The idea](#the-idea)
- [The data](#the-data)
- [How I approached it](#how-i-approached-it)
- [What I found](#what-i-found)
- [Comparing the methods](#comparing-the-methods)
- [How to run it](#how-to-run-it)

## The idea

I was curious about whether mall customers could be grouped in meaningful ways. I focused on just two things - how much they earn and how much they spend. It seemed like those two factors alone could tell you a lot about different customer types.

Some people make good money but are careful spenders, others spend freely even on modest incomes. If you treat everyone the same, you miss these important differences. I decided to try clustering - specifically K-Means (the standard approach) and DBSCAN (which doesn't force everyone into clusters). I was curious to see which would work better.

## The data

I used a dataset with 200 mall customers that includes:
- Customer ID
- Gender
- Age
- Annual Income (in thousands)
- Spending Score (1-100 scale)

I only used the income and spending score for clustering since those seemed most relevant for segmentation. The data was pretty clean - no missing values to deal with.

## How I approached it

First, I had to standardize the features because income numbers are way bigger than spending scores. Without scaling, the algorithm would just focus on income and ignore spending patterns.

For K-Means, I needed to figure out how many clusters to use. I tried the elbow method and silhouette analysis:
- Elbow method showed the "bend" around k=5
- Silhouette scores confirmed k=5 gave the best separation

For DBSCAN, I used a k-distance graph to pick the right eps parameter. I set min_samples to 5 and eps to 0.5 based on the distance plot.

## What I found

### K-Means Results (k=5)
The clusters actually made a lot of sense:

- **Cluster 0** (81 customers): High income, low spending - the "careful high earners"
- **Cluster 1** (39 customers): Low income, low spending - budget-conscious customers  
- **Cluster 2** (22 customers): High income, high spending - the "big spenders"
- **Cluster 3** (35 customers): Low income, high spending - "spend beyond means" group
- **Cluster 4** (23 customers): Medium income, medium spending - the "balanced" group

The visualization was really clear - you could see distinct groups with different colored points and cluster centers marked with X's.

### DBSCAN Results
DBSCAN found 3 clusters plus some noise points:
- **Cluster 0** (157 customers): The main group
- **Cluster 1** (35 customers): A smaller distinct group  
- **Noise** (8 customers): Outliers that didn't fit well

## Comparing the methods

K-Means was definitely cleaner and more business-friendly:
- Balanced cluster sizes
- Easy to interpret and explain
- No "noise" points to deal with
- Clear cluster centers

DBSCAN was more flexible but messier:
- Found natural groupings without forcing structure
- Identified outliers as noise
- But the results were harder to use for business decisions
- One huge cluster (157 customers) and one tiny one (35 customers)

For this dataset, K-Means was the better choice. The data seemed to have natural groupings that K-Means could capture well. DBSCAN might be better for messier, more irregular data.

## How to run it

You'll need these Python libraries:
```bash
pip install pandas numpy matplotlib scikit-learn
```

The notebook downloads the dataset automatically from a GitHub gist, so you don't need to worry about finding the data file. Just run all the cells and you'll see:
- Data loading and exploration
- Feature scaling
- Elbow method and silhouette analysis
- K-Means clustering with visualization
- DBSCAN clustering with visualization
- Comparison of both methods

## Key takeaways

The most interesting finding was that high-income customers aren't always big spenders. There's a whole group of people who earn well but spend carefully - that's valuable insight for marketing.

The "spend beyond means" group (low income, high spending) is also interesting - these might be customers to watch for credit risk.

K-Means worked really well here because the customer data had clear, distinct patterns. The silhouette score of 0.55 for k=5 was solid, and the visualizations made the clusters obvious.
