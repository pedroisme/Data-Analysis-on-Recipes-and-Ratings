
# The relationship between the recipe rating and the complexity of the recipe

Name(s): Jade Zhou / Zeyang Yu



---

## Introduction

Cooking is both an art and a science, and there are many factors that contribute to a recipe's success. One of these factors is the complexity of the recipe, which can be influenced by the number of ingredients, the amount of preparation time, and the level of difficulty in the cooking process. Another factor that can influence a recipe's success is the rating it receives from those who have tried it.

In this project, we will explore the relationship between the complexity of a recipe and the rating it receives. To do this, we will first need to perform data cleaning to ensure that our dataset is free of any errors. We will then assess missing data to determine whether it could affect our results , and if so, how to best address this issue. Finally, we will perform hypothesis testing to determine if there is a statistically significant relationship between the complexity of a recipe and its rating.

By analyzing the data in this way, we hope to gain a better understanding of the factors that contribute to a recipe's success and provide valuable insights for both home cooks and professional chefs alike.


---

## Cleaning and EDA

*This is the original dataframe before cleaning*
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>id</th>
      <th>minutes</th>
      <th>contributor_id</th>
      <th>submitted</th>
      <th>tags</th>
      <th>nutrition</th>
      <th>n_steps</th>
      <th>steps</th>
      <th>description</th>
      <th>ingredients</th>
      <th>n_ingredients</th>
      <th>rating</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1 brownies in the world    best ever</td>
      <td>333281</td>
      <td>40</td>
      <td>985201</td>
      <td>2008-10-27</td>
      <td>['60-minutes-or-less', 'time-to-make', 'course...</td>
      <td>[138.4, 10.0, 50.0, 3.0, 3.0, 19.0, 6.0]</td>
      <td>10</td>
      <td>['heat the oven to 350f and arrange the rack i...</td>
      <td>these are the most; chocolatey, moist, rich, d...</td>
      <td>['bittersweet chocolate', 'unsalted butter', '...</td>
      <td>9</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1 in canada chocolate chip cookies</td>
      <td>453467</td>
      <td>45</td>
      <td>1848091</td>
      <td>2011-04-11</td>
      <td>['60-minutes-or-less', 'time-to-make', 'cuisin...</td>
      <td>[595.1, 46.0, 211.0, 22.0, 13.0, 51.0, 26.0]</td>
      <td>12</td>
      <td>['pre-heat oven the 350 degrees f', 'in a mixi...</td>
      <td>this is the recipe that we use at my school ca...</td>
      <td>['white sugar', 'brown sugar', 'salt', 'margar...</td>
      <td>11</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>412 broccoli casserole</td>
      <td>306168</td>
      <td>40</td>
      <td>50969</td>
      <td>2008-05-30</td>
      <td>['60-minutes-or-less', 'time-to-make', 'course...</td>
      <td>[194.8, 20.0, 6.0, 32.0, 22.0, 36.0, 3.0]</td>
      <td>6</td>
      <td>['preheat oven to 350 degrees', 'spray a 2 qua...</td>
      <td>since there are already 411 recipes for brocco...</td>
      <td>['frozen broccoli cuts', 'cream of chicken sou...</td>
      <td>9</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>millionaire pound cake</td>
      <td>286009</td>
      <td>120</td>
      <td>461724</td>
      <td>2008-02-12</td>
      <td>['time-to-make', 'course', 'cuisine', 'prepara...</td>
      <td>[878.3, 63.0, 326.0, 13.0, 20.0, 123.0, 39.0]</td>
      <td>7</td>
      <td>['freheat the oven to 300 degrees', 'grease a ...</td>
      <td>why a millionaire pound cake?  because it's su...</td>
      <td>['butter', 'sugar', 'eggs', 'all-purpose flour...</td>
      <td>7</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2000 meatloaf</td>
      <td>475785</td>
      <td>90</td>
      <td>2202916</td>
      <td>2012-03-06</td>
      <td>['time-to-make', 'course', 'main-ingredient', ...</td>
      <td>[267.0, 30.0, 12.0, 12.0, 29.0, 48.0, 2.0]</td>
      <td>17</td>
      <td>['pan fry bacon , and set aside on a paper tow...</td>
      <td>ready, set, cook! special edition contest entr...</td>
      <td>['meatloaf mixture', 'unsmoked bacon', 'goat c...</td>
      <td>13</td>
      <td>5.0</td>
    </tr>
  </tbody>
</table>
</div>


1. A column called "Good or Bad'' is assigned to the data dataframe, indicating the rating is good or bad. If the average rating for a recipe is higher or equal to 3, then we consider the recipe as a good rating recipe. If the average rating for a recipe is lower than 3, then we consider it as a bad rating recipe.
2. The "ingredients" column is given as a string. We convert this string into a list; each element in this list is a string with one ingredient name. 
3. Similar to "ingredients", "nutrition" is also given as a string. We convert this string into a list; each element in this list is a float representing one nutrition value.
4. We drop several rows because we consider them as outliers. To be more specific, we removed several recipes from the data dataframe because those recipes have abnormal calorie values. An adult is recommended to eat 1600-2400 calories per day, therefore we set 2400 as a threshold. If a recipe has more than 2400 calories, we will remove that recipe, because it's very unusal.


*This is the clean dataframe*
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>id</th>
      <th>minutes</th>
      <th>contributor_id</th>
      <th>submitted</th>
      <th>tags</th>
      <th>nutrition</th>
      <th>n_steps</th>
      <th>steps</th>
      <th>description</th>
      <th>ingredients</th>
      <th>n_ingredients</th>
      <th>rating</th>
      <th>Good or Bad</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1 brownies in the world    best ever</td>
      <td>333281</td>
      <td>40</td>
      <td>985201</td>
      <td>2008-10-27</td>
      <td>['60-minutes-or-less', 'time-to-make', 'course...</td>
      <td>[138.4, 10.0, 50.0, 3.0, 3.0, 19.0, 6.0]</td>
      <td>10</td>
      <td>['heat the oven to 350f and arrange the rack i...</td>
      <td>these are the most; chocolatey, moist, rich, d...</td>
      <td>[bittersweet chocolate', 'unsalted butter', 'e...</td>
      <td>9</td>
      <td>4.0</td>
      <td>Good</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1 in canada chocolate chip cookies</td>
      <td>453467</td>
      <td>45</td>
      <td>1848091</td>
      <td>2011-04-11</td>
      <td>['60-minutes-or-less', 'time-to-make', 'cuisin...</td>
      <td>[595.1, 46.0, 211.0, 22.0, 13.0, 51.0, 26.0]</td>
      <td>12</td>
      <td>['pre-heat oven the 350 degrees f', 'in a mixi...</td>
      <td>this is the recipe that we use at my school ca...</td>
      <td>[white sugar', 'brown sugar', 'salt', 'margari...</td>
      <td>11</td>
      <td>5.0</td>
      <td>Good</td>
    </tr>
    <tr>
      <th>2</th>
      <td>412 broccoli casserole</td>
      <td>306168</td>
      <td>40</td>
      <td>50969</td>
      <td>2008-05-30</td>
      <td>['60-minutes-or-less', 'time-to-make', 'course...</td>
      <td>[194.8, 20.0, 6.0, 32.0, 22.0, 36.0, 3.0]</td>
      <td>6</td>
      <td>['preheat oven to 350 degrees', 'spray a 2 qua...</td>
      <td>since there are already 411 recipes for brocco...</td>
      <td>[frozen broccoli cuts', 'cream of chicken soup...</td>
      <td>9</td>
      <td>5.0</td>
      <td>Good</td>
    </tr>
    <tr>
      <th>3</th>
      <td>millionaire pound cake</td>
      <td>286009</td>
      <td>120</td>
      <td>461724</td>
      <td>2008-02-12</td>
      <td>['time-to-make', 'course', 'cuisine', 'prepara...</td>
      <td>[878.3, 63.0, 326.0, 13.0, 20.0, 123.0, 39.0]</td>
      <td>7</td>
      <td>['freheat the oven to 300 degrees', 'grease a ...</td>
      <td>why a millionaire pound cake?  because it's su...</td>
      <td>[butter', 'sugar', 'eggs', 'all-purpose flour'...</td>
      <td>7</td>
      <td>5.0</td>
      <td>Good</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2000 meatloaf</td>
      <td>475785</td>
      <td>90</td>
      <td>2202916</td>
      <td>2012-03-06</td>
      <td>['time-to-make', 'course', 'main-ingredient', ...</td>
      <td>[267.0, 30.0, 12.0, 12.0, 29.0, 48.0, 2.0]</td>
      <td>17</td>
      <td>['pan fry bacon , and set aside on a paper tow...</td>
      <td>ready, set, cook! special edition contest entr...</td>
      <td>[meatloaf mixture', 'unsmoked bacon', 'goat ch...</td>
      <td>13</td>
      <td>5.0</td>
      <td>Good</td>
    </tr>
  </tbody>
</table>
</div>
**Univariate Analysis**



This histogram demonstrates the distribution of the number of steps each recipe has. The plot is right skewed and has the peak at around 10 steps. Recipes with around 10 steps have the largest share of the overall dataset. We can also learn that most recipes have less than 20 steps and an extremely small number of recipes have more than 40 steps.

<iframe src="step.html" width=800 height=600 frameBorder=0></iframe>

This histogram demonstrates the distribution of the number of ingredients each recipe has. The plot is right skewed and has the peak at around 7 ingredients. It also shows that most recipes have around 5 to 12 ingredients and an extremely small number of recipes have more than 20 ingredients.

<iframe src="rating.html" width=800 height=600 frameBorder=0></iframe>

This histogram demonstrates the distribution of the average rating of each recipe. The plot doesn’t have a distinct trend. Rating 4 and 5 have great proportions because some recipes only have one rating, so it remains as an integer. Some other recipes are taking the mean of all ratings, so the values will be more spread out. But overall from the plot we can learn that a large amount of the recipes have high ratings (4-5).


<iframe src="ingredients.html" width=800 height=600 frameBorder=0></iframe>

**Bivariate Analysis**

This scatter plot demonstrates the relationship between recipe rating and how many steps it takes, where x-axis represents the rating and y-axis represents the number of steps. From the shade of the cluster, we can expect that a recipe with less ingredients is likely to get a higher rating, but it's very unsure. The plot doesn't show any clear trend and the data clusters at integer value of rating, so it's hard to analyze the plot. 

<iframe src="BA1.html" width=800 height=600 frameBorder=0></iframe>

This scatter plot demonstrates the relationship between recipe rating and how many ingredients it needs, where x-axis represents the number of ingredients needed and y-axis represents the rating. We noticed that the data clusters are at the range between 0-20 ingredients and 4-5 ratings.
<iframe src="BA2.html" width=800 height=600 frameBorder=0></iframe>

**interesting aggregate**

We grouped by the n_steps column and get the mean of other column values. By doing this, we separate the 8 million recipes we have into groups based on the number of their cooking steps. And we can easily access the mean rating (as well as cooking time, n_ingredients) for each group.

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>minutes</th>
      <th>contributor_id</th>
      <th>n_ingredients</th>
      <th>rating</th>
    </tr>
    <tr>
      <th>n_steps</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>376049.162261</td>
      <td>31.196901</td>
      <td>8.795520e+06</td>
      <td>5.659982</td>
      <td>4.455765</td>
    </tr>
    <tr>
      <th>2</th>
      <td>377193.279739</td>
      <td>35.173830</td>
      <td>7.846780e+06</td>
      <td>6.032233</td>
      <td>4.481502</td>
    </tr>
    <tr>
      <th>3</th>
      <td>375429.054128</td>
      <td>50.255924</td>
      <td>6.814714e+06</td>
      <td>6.540284</td>
      <td>4.447997</td>
    </tr>
    <tr>
      <th>4</th>
      <td>376513.659186</td>
      <td>85.991460</td>
      <td>5.751555e+06</td>
      <td>7.152135</td>
      <td>4.413163</td>
    </tr>
    <tr>
      <th>5</th>
      <td>377126.818122</td>
      <td>82.942055</td>
      <td>1.005128e+07</td>
      <td>7.640020</td>
      <td>4.369643</td>
    </tr>
  </tbody>
</table>
</div>

---

## Assessment of Missingness
**NMAR Analysis**
The rating value missing is NMAR in this recipe dataset. We expect that the missingness will have some relations with one or several other columns, because during the data collecting process (when people submit reviews), rating is very important and easy to write down, so people are less likely to skip this part. Compared to writing comments, rating has a low chance to be lost. But we need to include more data to figure out what exactly the missingness type is, such as consumers ' age and how they are familiar with the review system. The rating might be missed during the data collection because the consumer unintentionally skipped this step.

**Missingness Dependency Analysis**

We work on the missingness of rating. We think it might be related to the number of steps and number of ingredients each recipe has, therefore we will take a look at those two columns separately. We formed a new dataframe called Data_missingness which only includes the information we need for the missingness analysis.
*Dataframe*
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>n_steps</th>
      <th>n_ingredients</th>
      <th>rate missing</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10</td>
      <td>9</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>12</td>
      <td>11</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>6</td>
      <td>9</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>7</td>
      <td>7</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>17</td>
      <td>13</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>
<iframe src="fig_Missingness.html" width=800 height=600 frameBorder=0></iframe>

<iframe src="fig_Missingness2.html" width=800 height=600 frameBorder=0></iframe>

Those two histograms demonstrate the distribution of the two selected columns (number of steps and number of ingredients) when the rating is missing and when the rating is not missing. We can tell from the plot that there are some differences, but we are not sure how big the difference is. Therefore, we run permutation tests for the two selected columns separately, and here are the results:

<iframe src="fig_permutation_ingredients.html" width=800 height=600 frameBorder=0></iframe>


<iframe src="fig_permutation_steps.html" width=800 height=600 frameBorder=0></iframe>

The histogram shows the distribution of the difference of mean of the two selected columns when the rating is missing and not missing. The red vertical represents the observed stats.
For the n_steps plot, we can tell there is a huge gap between the observed value and the permutation distribution, therefore we can easily conclude that n_steps for rating missing recipes and n_steps for rating NOT missing recipes do not come from the same population. To be more straightforward, the missingness of rating is related to n_steps.
For the n_ingredients plot, the observed value falls in the permutation distribution, therefore we cannot conclude that n_ingredients for rating missing recipes and n_ingredients for rating NOT missing recipes do not come from the same population. So we cannot get the conclusion that the missingness of rating is related to n_ingredients.
In conclusion: the missingness of rating is related to n_steps,  but the missingness of rating is not necessarily related to n_ingredients.
---

## Hypothesis Testing
Null hypothesis: There is no significant relationship between the cooking step and rating of recipes.
Alternative hypothesis: There is a significant relationship between the cooking step and rating of recipes.
To be more specific, we expect that the cooking steps do not influence whether the rating is good or bad if we fail to reject null. But if we decide that we need to reject null after the permutation test, then it means the cooking step and rating of recipes have some relationships and one variable influences the other.

*Here are the head of two selected columns from the dataframe:*

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>n_steps</th>
      <th>Good or Bad</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10</td>
      <td>Good</td>
    </tr>
    <tr>
      <th>1</th>
      <td>12</td>
      <td>Good</td>
    </tr>
    <tr>
      <th>2</th>
      <td>6</td>
      <td>Good</td>
    </tr>
    <tr>
      <th>3</th>
      <td>7</td>
      <td>Good</td>
    </tr>
    <tr>
      <th>4</th>
      <td>17</td>
      <td>Good</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>Good</td>
    </tr>
    <tr>
      <th>6</th>
      <td>4</td>
      <td>Bad</td>
    </tr>
    <tr>
      <th>7</th>
      <td>10</td>
      <td>Good</td>
    </tr>
    <tr>
      <th>8</th>
      <td>10</td>
      <td>Good</td>
    </tr>
    <tr>
      <th>9</th>
      <td>14</td>
      <td>Good</td>
    </tr>
  </tbody>
</table>
</div>

The observed statistics we chose is the difference of mean when the review is good and when the review is bad. The significance level is 0.05. 
We perform the permutation test here and we are trying to figure out whether n_steps data from good rating recipes and n_steps data from bad rating recipes come from the same population. From there, we can made the decision whether the relationship exists or not.

After running 1000 permutation test, the p-value we ended up getting a is 0. The p-value is smaller than the significance level, so we reject the null hypothesis.


<iframe src="fig_permutation_shuffled_steps.html" width=800 height=600 frameBorder=0></iframe>

From this plot, which demonstrates the distribution of the permutation tests with the observed stats as a vertical line. We learn that the observed stats are far away from the permutation result. So we can conclude there exists a relationship between the number of steps each recipe needs and whether the rating is good or bad. This conclusion we get from the plot matches with the rejection of the null hypothesis. In this case, our data science question is answered.
<!-- *final*

<iframe src="fig_final.html" width=800 height=600 frameBorder=0></iframe>
 -->

   
--- -->