import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
%matplotlib inline 
#extracting the files
tracks_df= pd.read_csv("C:/Users/Jyoti/Desktop/data set/tracks.csv")
tracks_df.head()
df_genre=pd.read_csv("C:/Users/Jyoti/Desktop/data set/SpotifyFeatures.csv")
df_genre.head()
#which singer has the most rows in data set 
topsinger= tracks_df.artists.value_counts().sort_values(ascending=False).head(1)
topsinger
#10 least popular songs 
least_popular=tracks_df.sort_values('popularity',ascending=True).head(10)
least_popular
#top 10 most popular songs 
most_popular=tracks_df.query('popularity>90',inplace=False).sort_values('popularity', ascending=False).head(10)
most_popular
sample_df=tracks_df.sample(int(0.004*len(tracks_df)))
print (len( sample_df))
tracks_df[["artists"]].iloc[18]
plt.figure(figsize=(10,6))
sns.regplot(data=sample_df, y= "loudness" , x= "energy", color="c").set(title="loudness vs energy correlation")
plt.figure(figsize=(10,6))
sns.regplot(data=sample_df, y= "popularity" , x= "acousticness", color="b").set(title="popularity vs acoustinesscorelation")
tracks_df['duration']= tracks_df["duration_ms"].apply(lambda x: round(x/1000))
tracks_df.drop("duration_ms", inplace=True, axis=1)
tracks_df.duration.head()
plt.title("duration of songs in different genres")
sns.color_palette("rocket", as_cmap=True)
sns.barplot( y= 'genre',x='duration_ms', data= df_genre)
plt.xlabel("duration_ms")
plt.ylabel("genres")
sns.set_style(style="darkgrid")
plt.figure(figsize=(10,5))
famous=df_genre.sort_values('popularity',ascending=False).head(10)
sns.barplot(y='genre', x='popularity',data= famous).set(title="top 5 genres by popularity")
