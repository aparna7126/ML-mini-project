# ML-mini-project
# Movie Recommendation System Using Content-Based and Collaborative Filtering

**One-line summary:** A movie recommendation system built using the MovieLens dataset that recommends movies based on user ratings and movie genres. The content-based model achieved an RMSE of 0.9414, compared with the user-mean baseline RMSE of 0.9662.

## 1. Problem

Users often find it difficult to discover movies that match their interests because of the large number of available movies. This project develops a recommendation system that predicts user preferences and suggests movies they may enjoy.

**Objectives:**
- Recommend movies based on genres and user rating history.
- Identify similarities between movies.
- Predict ratings using collaborative filtering and SVD.
- Compare recommendation techniques using evaluation metrics.

## 2. Data

**Dataset:** MovieLens Latest Small (`ml-latest-small`)

**Source:** [GroupLens MovieLens Dataset](https://grouplens.org/datasets/movielens/latest/)

| Attribute | Value |
|---|---:|
| Users | 610 |
| Movies | 9,742 |
| Ratings | 100,836 |
| Rating scale | 0.5–5.0 |
| Tag applications | 3,683 |
| Sparsity | Approximately 98.30% |

**Dataset files:**
- `movies.csv` – Movie IDs, titles, and genres.
- `ratings.csv` – User ratings and timestamps.
- `tags.csv` – User-generated movie tags.
- `links.csv` – External movie identifiers.

The dataset is provided by GroupLens for research purposes. Refer to its official website for usage conditions.

## 3. Method

The project implements the following techniques:

1. **Baseline models:** Global mean, user mean, and movie mean predictions.
2. **Content-based filtering:** Uses TF-IDF to represent movie genres and cosine similarity to identify similar movies.
3. **Item-based collaborative filtering:** Uses similarities between movies based on user ratings.
4. **SVD:** Uses Truncated Singular Value Decomposition to predict missing ratings.
5. **Hybrid recommendation:** Combines collaborative and content-based predictions using 70% collaborative and 30% content-based weighting.

### Data Splitting

- Ratings were divided into training and testing sets.
- A time-based split was used for each user.
- The latest 20% of eligible users' ratings were selected for testing.
- Training data was used to build recommendation models.
- Test data was used for evaluation.

## 4. Results

### Model Comparison

| Model | RMSE | Precision@10 | Recall@10 | NDCG@10 |
|---|---:|---:|---:|---:|
| Global mean | 1.069 | 0.0022 | 0.0028 | 0.0037 |
| Most popular | 1.069 | 0.0574 | 0.0506 | 0.0759 |
| Content-based | 0.965 | 0.0019 | 0.0008 | 0.0022 |
| Collaborative filtering | 1.333 | 0.0002 | 0.0000 | 0.0001 |
| SVD (k=10) | 0.945 | 0.0697 | 0.0549 | 0.0899 |

### Additional Hybrid Experiment

| Model | RMSE |
|---|---:|
| Content-based | 0.9414 |
| Collaborative filtering | 0.9619 |
| Hybrid (70% CF + 30% content) | 0.9492 |

The content-based model achieved the lowest RMSE in the additional experiment. It improved over the user-mean baseline (0.9662) by 0.0248.

**Note:** The Section 8 and Section 9 content-based results come from separate prediction calculations. The most-popular model is primarily a ranking model, so its RMSE was set to the global mean for the Section 8 comparison.

### Recommendation Demo

The system generates personalized movie recommendations for an existing user while excluding movies they have already rated.

Add your actual recommendation screenshot here:

`![Movie Recommendation Demo](screenshots/recommendation-demo.png)`

## 5. Understanding Pack

### By-Hand Verification

A user-mean prediction was manually verified.

- User ID: 1
- Sum of training ratings: 813
- Number of training ratings: 186
- Manual user mean: 4.371
- Code prediction: 4.371
- Difference: 0.0

The manual calculation matched the code prediction.

### Deliberate Data Leakage Experiment

Compared training-only statistics with full-dataset statistics.

| Approach | Test RMSE |
|---|---:|
| Honest training-only mean | 1.0694 |
| Leaked full-data mean | 1.0687 |

The leaked result showed an RMSE decrease of 0.0007. However, it is not a fair evaluation because test-set information was used.

### Break-It Tests

The following cases were tested:

- **New user:** Checks how the system handles an unknown user.
- **Unknown movie:** Checks whether a movie ID exists in the dataset.
- **User with one training rating:** Checks recommendation behaviour with limited rating history.
- **All ratings equal to 5:** Tests extreme rating values and restores the original ratings afterward.

## 6. Limitations

- The dataset is relatively small compared with real-world recommendation platforms.
- New users and movies may have insufficient information for accurate recommendations.
- Movie genres alone cannot capture every aspect of user preferences.
- Recommendation quality depends on available rating history.
- The project does not use real-time user activity.
- The hybrid model did not outperform the content-based model in the additional RMSE experiment.

## 7. AI-Use Note

ChatGPT was used to assist with:
- Data preprocessing and exploratory data analysis.
- Baseline model implementation.
- TF-IDF and cosine similarity.
- Collaborative filtering and SVD.
- Evaluation, debugging, and hybrid recommendation code.

All code was executed and checked using Google Colab. Dataset statistics, model outputs, RMSE values, recommendations, and manual calculations were verified.

One identified issue was a user ID type mismatch in the recommendation function. It was corrected by converting user IDs to strings using `str(user)`.

## 8. How to Run

**Requirements:**
- Python 3
- Google Colab or Jupyter Notebook
- NumPy
- Pandas
- Matplotlib
- Scikit-learn

### Steps

1. Download the `ml-latest-small.zip` dataset from [GroupLens](https://grouplens.org/datasets/movielens/latest/).
2. Open the project notebook in Google Colab.
3. Upload the dataset ZIP file when prompted.
4. Run the notebook cells sequentially.
5. Execute the recommendation demo cell.
6. View the recommended movies for the selected user.

**Google Colab Notebook:** Add your shared notebook link here.

---

**Project:** Movie Recommendation System  
**Dataset:** MovieLens Latest Small  
**Tools:** Python, Google Colab, Pandas, NumPy, Matplotlib, Scikit-learn  
**Techniques:** Content-Based Filtering, Collaborative Filtering, SVD, Hybrid Recommendation
