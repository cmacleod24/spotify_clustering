# spotify_clustering

Spotify Sound Profiles: Clustering Songs by Audio Features

Research question

Can Spotify audio features group songs into sound profiles that go beyond genre labels, and could those profiles be used to create playlists or recommendations?

Here, a sound profile is a group of songs with similar values across a set of audio features. Each k-means cluster is treated as one sound profile.

Module_3_Assignment.ipynb runs the following steps in order:

Load and clean the data. It removes the row with a missing track name or artist, keeps only songs listed under exactly one genre, and drops repeated track IDs and repeated track name + artist pairs.
Sample 500 songs from each genre that still has at least 500 songs after cleaning (78 genres, 39,000 songs, random seed 42).
Prepare features. Duration is log-transformed because a few extremely long tracks formed their own cluster. All features are then standardized with StandardScaler.
Choose k. The notebook plots inertia for k = 2 to 15 (elbow plot), then compares k = 7 and k = 8 by cluster sizes and average feature values. k = 8 was chosen.
Fit k-means with k = 8 (Euclidean distance).
Describe the clusters. For each cluster, the notebook prints the top genres and the two songs closest to the cluster center, then builds a summary table of average feature values with a descriptive label per cluster.

Features used for clustering: danceability, energy, loudness, speechiness, acousticness, instrumentalness, liveness, valence, tempo, and duration (log-transformed).

Columns left out of the clustering:
popularity: measures listener behavior, not sound.
key and time_signature: categorical codes that Euclidean distance would treat as quantities.
mode and explicit: included at first, but they split nearly identical sound profiles into separate clusters, so they were removed.
track_genre, track name, and artists: used only afterward to describe and check the clusters.

Most clusters mix unrelated genres. 

Data
Dataset: Spotify Tracks Dataset by MaharshiPandya on Kaggle (114,000 tracks across 114 genres).
Audio features are Spotify's own measurements, and I did not collect the original data. See the dataset's Kaggle page for how it was gathered: https://www.kaggle.com/datasets/maharshipandya/-spotify-tracks-dataset?resource=download

How to run
Clone this repository or download the notebook.
Download dataset.csv from the Kaggle link above and put it next to the notebook.
Install the requirements:
   pip install pandas numpy scikit-learn matplotlib jinja2

jinja2 is needed for the styled summary table at the end of the notebook. 4. Open the notebook in Jupyter or Google Colab and run all cells from top to bottom. 

Reproducibility notes
Sampling and k-means use random_state=42, so the cluster sizes should match the table above if you start from the same file. Cluster numbers (0 to 7) can change if the data or settings change.

Limitations
No listener data, so the analysis cannot show whether sound-based playlists or recommendations would work for listeners.
Ten summary audio features are not all encompassing.
Sampling the same number of songs per genre does not reflect the real mix of music on Spotify, and 36 genres were excluded because cleaning left them with fewer than 500 songs.
Keeping only single-genre songs removed some of the genre overlap in the original data.
The elbow was gradual, so choosing k = 8 over k = 7 involved judgment.
