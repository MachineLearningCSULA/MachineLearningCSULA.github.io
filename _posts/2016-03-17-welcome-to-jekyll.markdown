---
layout: post
title:  "Data Munging"
categories: jekyll update
---
<!-- You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. You can rebuild the site in many different ways, but the most common way is to run `jekyll serve`, which launches a web server and auto-regenerates your site when a file is updated.

To add new posts, simply add a file in the `_posts` directory that follows the convention `YYYY-MM-DD-name-of-post.ext` and includes the necessary front matter. Take a look at the source for this post to get an idea about how it works.

Jekyll also offers powerful support for code snippets:

{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: http://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/ -->
<hr>
{% highlight ruby %}
Data was not organized in the manner that we needed to consume it.  We passed
lists of films organized by date through a rest service built to query imdb.
The result is matrix of features that we used in our analysis.  We used
a combination of logic written in python and java to clean and organize the
results.  
{% endhighlight %}
The code for extraction is available here 
[Data Munging](https://github.com/MachineLearningCSULA/DataMunging)
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
 loop to make multiple rest calls to twitter's rest api.  The tweets were 
 feed through a method in textblob that returned sentiment analysis based
 on sophisticated implementation of Naive Bayes which returned a score 
 between -1 and 1.  If the score was less then one we could assume 
 that the movie negative sentiments on twitter and greater then
 positive.  This score was then averaged and scaled and added to 
 a column in our matrix of features. 
{% endhighlight %}
