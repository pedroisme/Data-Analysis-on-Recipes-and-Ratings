
# The relationship between the recipe rating and the complexity of the recipe

Name(s): Jade Zhou / Zeyang Yu



---

## Introduction

Cooking is both an art and a science, and there are many factors that contribute to a recipe's success. One of these factors is the complexity of the recipe, which can be influenced by the number of ingredients, the amount of preparation time, and the level of difficulty in the cooking process. Another factor that can influence a recipe's success is the rating it receives from those who have tried it.

In this project, we will explore the relationship between the complexity of a recipe and the rating it receives. To do this, we will first need to perform data cleaning to ensure that our dataset is free of any errors. We will then assess missing data to determine whether it could affect our results , and if so, how to best address this issue. Finally, we will perform hypothesis testing to determine if there is a statistically significant relationship between the complexity of a recipe and its rating.

By analyzing the data in this way, we hope to gain a better understanding of the factors that contribute to a recipe's success and provide valuable insights for both home cooks and professional chefs alike.


---

## Cleaning and EDA
1. A column called "Good or Bad'' is assigned to the data dataframe, indicating the rating is good or bad. If the average rating for a recipe is higher or equal to 3, then we consider the recipe as a good rating recipe. If the average rating for a recipe is lower than 3, then we consider it as a bad rating recipe.
2. The "ingredients" column is given as a string. We convert this string into a list; each element in this list is a string with one ingredient name. 
3. Similar to "ingredients", "nutrition" is also given as a string. We convert this string into a list; each element in this list is a float representing one nutrition value.
4. We drop several rows because we consider them as outliers. To be more specific, we removed several recipes from the data dataframe because those recipes have abnormal calorie values. An adult is recommended to eat 1600-2400 calories per day, therefore we set 2400 as a threshold. If a recipe has more than 2400 calories, we will remove that recipe, because it's very unusal.

**Univariate Analysis**

*Univariate Analysis graphs*

This histogram demonstrates the distribution of the number of steps each recipe has. The plot is right skewed and has the peak at around 10 steps. Recipes with around 10 steps have the largest share of the overall dataset. We can also learn that most recipes have less than 20 steps and an extremely small number of recipes have more than 40 steps.

<iframe src="step.html" width=800 height=600 frameBorder=0></iframe>

This histogram demonstrates the distribution of the number of ingredients each recipe has. The plot is right skewed and has the peak at around 7 ingredients. It also shows that most recipes have around 5 to 12 ingredients and an extremely small number of recipes have more than 20 ingredients.

<iframe src="rating.html" width=800 height=600 frameBorder=0></iframe>

This histogram demonstrates the distribution of the average rating of each recipe. The plot doesn’t have a distinct trend. Rating 4 and 5 have great proportions because some recipes only have one rating, so it remains as an integer. Some other recipes are taking the mean of all ratings, so the values will be more spread out. But overall from the plot we can learn that a large amount of the recipes have high ratings (4-5).


<iframe src="ingredients.html" width=800 height=600 frameBorder=0></iframe>

*Bivariate Analysis*
This scatter plot demonstrates the relationship between recipe rating and how many steps it takes, where x-axis represents the rating and y-axis represents the number of steps. From the shade of the cluster, we can expect that a recipe with less ingredients is likely to get a higher rating, but it’s very unsure. The plot doesn’t show any clear trend and the data clusters at integer value of rating, so it’s hard to analyze the plot. 

<iframe src="BA1.html" width=800 height=600 frameBorder=0></iframe>

This scatter plot demonstrates the relationship between recipe rating and how many ingredients it needs, where x-axis represents the number of ingredients needed and y-axis represents the rating. We noticed that the data clusters are at the range between 0-20 ingredients and 4-5 ratings.
<iframe src="BA2.html" width=800 height=600 frameBorder=0></iframe>


---

## Assessment of Missingness

<iframe src="fig_Missingness.html" width=800 height=600 frameBorder=0></iframe>

<iframe src="fig_Missingness2.html" width=800 height=600 frameBorder=0></iframe>


---

## Hypothesis Testing
*Permutation*
<iframe src="fig_permutation_ingredients.html" width=800 height=600 frameBorder=0></iframe>


<iframe src="fig_permutation_steps.html" width=800 height=600 frameBorder=0></iframe>


<iframe src="fig_permutation_shuffled_steps.html" width=800 height=600 frameBorder=0></iframe>


*final*

<iframe src="fig_final.html" width=800 height=600 frameBorder=0></iframe>

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
---