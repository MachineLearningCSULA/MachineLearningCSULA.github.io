---
layout: post
title:  "Data Munging"
categories: jekyll update
---
<hr>
{% highlight ruby %}
Data was not organized in the manner that we needed to consume it.  We passed
lists of films organized by date through a rest service built to query imdb.
The result is matrix of features that we used in our analysis.  We used
a combination of logic written in python and java to clean and organize the
results.  
{% endhighlight %}
The code for extraction is available here 
[Data Munging](https://github.com/MachineLearningCSULA/DataMunging_V2)
<h1>Our Data Sets</h1>
<hr>
<table>
<tr>
    <th>title</th>
    <th>year</th>
    <th>released</th>
    <th>genre</th>
    <th>rated</th>
    <th>runtime</th>
    <th>language</th>
    <th>director</th>
    <th>writer</th>
    <th>metascore</th>
    <th>rating</th>
    <th>votes</th>
    <th>budget</th>
    <th>gross</th>
</tr>
{% for movie in site.data.movies limit:10  %}
      <tr>  
        <td>{{ movie.title }}</td>
        <td>{{ movie.year }}</td>
        <td>{{ movie.released_month }}</td>
        <td>{{ movie.genre }}</td>
        <td>{{ movie.rated }}</td>
        <td>{{ movie.runtime }}</td>
        <td>{{ movie.language }}</td>
        <td>{{ movie.director }}</td>
        <td>{{ movie.writer }}</td>
        <td>{{ movie.metascore }}</td>
        <td>{{ movie.rating }}</td>
        <td>{{ movie.votes }}</td>
        <td>{{ movie.budget }}</td>
        <td>{{ movie.gross }}</td>
      </tr>
{% endfor %}
</table>
<br>
<h1>Collecting Data for sentiment analysis from twitter</h1>
<hr>
{% highlight ruby %}
 To make the analysis more robust we decided that a column should be added 
 for each film that would use sentiment analysis to infer if social media
 had any impact on a films success.  Our list of films was feed through a 
 loop to make multiple rest calls to twitter's rest api. Due to limitations
 in twitter data access, 100 tweets per each movie were analyzed.
{% endhighlight %}
<h2>Positive vs Negative Sentiment</h2>
<img src="/assets/pos_neg.png"/>
<br>
<h3>Example Data: Straight Outta Compton (2015)</h3>
<hr>
<img src="/assets/sentimentchart.jpg" />
<br>
{% highlight ruby %}
 The tweets were feed through a method in textblob that returned 
 sentiment analysis based on sophisticated implementation of Naive 
 Bayes which returned a score between -1 and 1. 
 In order to give fair scoring, only unique tweets per each movie were counted, 
 and sentences with neutral sentiment (usually advertisement or links) were not counted towards 
 calculating an average. This score was then averaged and scaled and added to a column 
 in our matrix of features. 
{% endhighlight %}
<br><br>
<img src="/assets/sentimentchart2.jpg" />
<br>
{% highlight ruby %}
 Since social media tweets are unstructured sentences that contain
 special characters, mispelled words and slangs, sorting out meaningful
 sentences were a challenge. Also textblob library failed to provide
 accurate analysis on sentences that contain both positive and negative words.
{% endhighlight %}
<br><br>
<img src="/assets/straight_result.jpg" />
<br>
{% highlight ruby %}
 The movie Straight Outta Compton receives average sentiment score of +30.
{% endhighlight %}
<br><br>


