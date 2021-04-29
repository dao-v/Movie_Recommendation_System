# Movie Recommendation System:

This script was designed to predict the ratings of movies unseen by users according to the genres and tags associated with the movies they've liked and disliked. The dataset was obtained from grouplens (University of Minnesota, https://grouplens.org/datasets/movielens/), specifically the "MovieLens 25M Dataset": http://files.grouplens.org/datasets/movielens/ml-25m.zip (250 MB)<br>
The resulting DataFrame produced by this script will choose the top ten movies with the highest predicted ratings.

To see a more step-by-step walkthrough of the code, see my Medium post: https://medium.com/@dv930/recommendation-system-for-movies-movielens-grouplens-171d30be334e

## Predictive Model Design:
Predictions are a result of three models. The first model feeds in the genres from the movies that the like and disliked + the genres of the movie in question into a neural network/deep learning model and outputs a predicted rating. The second model is similar to the first model except it uses the tags associated with the movies that have been watched by the user and the tags associated with the movie in question to predict a rating. The third model takes the two predicted ratings from the first two models and predicts a final rating using linear regression.

There is a potential that not all users will be included in this script because if a user had only watched one movie with little to no tags, it would not be possible to input them into the tags model.

(Files: links.csv, genome-scores.csv, and genome-tags.csv are not used in this script)

## How to Use:
- To begin using this script, download the "MovieLens 25M Dataset" and extract the file (ml-23m) into the same directory where this script is located.
- [Optional] Second, also unzip data.zip (from the GitHub repository) into the same directory as well.
- Next, simply run all the cells in this notebook and all additional folders will be produced as needed. 
- Lastly, the top ten movies (as well as the predictions for all movies for a specific user) will be displayed in cells 20-22, using the userId of 6550 as an example. These two DataFrames will not be saved automatically and will only be there to show the results. 

## Things to Note:
- All users are included in the statistics in cell 18, including those who've only rated a couple of movies. Most recommendation systems will attempt to address this by copying other users' profiles who've watched/rated the same movies over to the user with fewer data. This script does not directly deal with users with low data--instead, the movie(s) that the users did watch will have a majority (or sole) impact on what the models will predict.
- Most of the cells will finish running within a couple of hours at most. However, cell 13 will most likely run for over 2 days before finishing. A copy of the resulting DataFrame is included in the GitHub repository in the correct location for the script to find the CSV file. Unless the original dataset is different from "MovieLens 25M Dataset" or just wanting to fully run the entire script, removal of the triple quotes in cell 13 is needed before running.
- The very last cell (23) can be run to produce predictions for all users. However, the removal of the triple single quotes (comment syntax) is required before running.


## Minimum System Requirements & Runtimes (IMPORTANT):
Since the "ratings.csv" file is extremely large (25+ million rows), this script requires a large amount of RAM if using a personal system. My system has 48 GB of RAM and it is fully utilized during the model training for random forest (cell 18).  If you do not have that much RAM and (understandably) will not upgrade/add more RAM to your system, it is advised to splice a smaller subset of "ratings.csv" in cell 2 to a size that is more manageable to your system. In addition, setting a maximum length for each random forest tree and lower the number of trees trained in cell 18 might be required. From my experience, selecting a subset of "ratings.csv" for training does not seem to have a large impact on the performance of the models. If possible, loading in "ratings.csv" and shuffling it before subsetting is recommended since the CSV file is ordered by users.

The entire script (without cells 13 and 23) should finish running within a day if the system is up-to-date on hardware and no major background applications are running. This script was ran using the GPU version of TensorFlow. If you do not have TensorFlow installed + have a supported Nvidia GPU in your system + are using an Anaconda distribution, install TensorFlow GPU using the instructions by Anaconda: https://docs.anaconda.com/anaconda/user-guide/tasks/tensorflow/

The runtime for the last cell (cell 23) is expected to take many days.

All components created and the original dataset will take up about 2.13 GB of storage. Running cell 23 is estimated to additionally take about 150 MB of storage.


(No Python parallel programming is used in this script. Full CPU utilization is only used by Sklearn during the random forest training.)

To compare, my system specifications are: <br>
CPU = Intel i5-9600k (6-cores, factory settings) <br>
GPU = Nvidia RTX 2070<br>
Primary Storage Device = NVMe, Western Digital Black SN750<br>
RAM Speed = DDR4 3000


<br><br><br><br>
VERSION 1.01<br><br>
Version 1.01 Updates:<br>
~ Changed all "\\" to "/" (for universial usage in Windows and Linux)<br>
~ Changed all "to_csv()" to include the "index = False" argument<br>
~ Changed all "read_csv()" to remove all "index_col = 0" argument<br>
~ "common_tags_df" creation fixed ("tag" column was becoming a index when using ".groupby()")<br>
~ Exporting vectorized_dict dictionary as a pickle file (as well as loading it in). Adding the pickle file to data.zip<br>

<br><br>
Questions? Comments? Email me: dv930@nyu.edu
