
# Dictionaries

Another built in python data structure is the dictionary. Dictionaries creating mappings between key value pairs like so:  
`dict1 = {keyX : valueX, keyC : valueC, keyQ : valueQ}`. 

you could also create the same dictionary like this:  
`dict1 = dict(keyX : valueX, keyC : valueC, keyQ : valueQ)`. 

Unlike strings or lists, dictionaries do not have an index or a specific order. There are ways to iterate through a dictionary, but the order that the items are returned is not gauranteed to be in a specific order. Instead, dictionaries are good for finding the value of a specific item rather then an item in a specific place.  

Let's look at a couple of examples in practice:

# Importing Packages and Data
As usual, let's start by import pandas and some data that we would be working with.


```python
import pandas as pd
```


```python
df = pd.read_csv('lego_sets.csv')
df.head()
```




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
      <th>ages</th>
      <th>list_price</th>
      <th>num_reviews</th>
      <th>piece_count</th>
      <th>play_star_rating</th>
      <th>prod_desc</th>
      <th>prod_id</th>
      <th>prod_long_desc</th>
      <th>review_difficulty</th>
      <th>set_name</th>
      <th>star_rating</th>
      <th>theme_name</th>
      <th>val_star_rating</th>
      <th>country</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>6-12</td>
      <td>29.99</td>
      <td>2.0</td>
      <td>277.0</td>
      <td>4.0</td>
      <td>Catapult into action and take back the eggs fr...</td>
      <td>75823.0</td>
      <td>Use the staircase catapult to launch Red into ...</td>
      <td>Average</td>
      <td>Bird Island Egg Heist</td>
      <td>4.5</td>
      <td>Angry Birds™</td>
      <td>4.0</td>
      <td>US</td>
    </tr>
    <tr>
      <th>1</th>
      <td>6-12</td>
      <td>19.99</td>
      <td>2.0</td>
      <td>168.0</td>
      <td>4.0</td>
      <td>Launch a flying attack and rescue the eggs fro...</td>
      <td>75822.0</td>
      <td>Pilot Pig has taken off from Bird Island with ...</td>
      <td>Easy</td>
      <td>Piggy Plane Attack</td>
      <td>5.0</td>
      <td>Angry Birds™</td>
      <td>4.0</td>
      <td>US</td>
    </tr>
    <tr>
      <th>2</th>
      <td>6-12</td>
      <td>12.99</td>
      <td>11.0</td>
      <td>74.0</td>
      <td>4.3</td>
      <td>Chase the piggy with lightning-fast Chuck and ...</td>
      <td>75821.0</td>
      <td>Pitch speedy bird Chuck against the Piggy Car....</td>
      <td>Easy</td>
      <td>Piggy Car Escape</td>
      <td>4.3</td>
      <td>Angry Birds™</td>
      <td>4.1</td>
      <td>US</td>
    </tr>
    <tr>
      <th>3</th>
      <td>12+</td>
      <td>99.99</td>
      <td>23.0</td>
      <td>1032.0</td>
      <td>3.6</td>
      <td>Explore the architecture of the United States ...</td>
      <td>21030.0</td>
      <td>Discover the architectural secrets of the icon...</td>
      <td>Average</td>
      <td>United States Capitol Building</td>
      <td>4.6</td>
      <td>Architecture</td>
      <td>4.3</td>
      <td>US</td>
    </tr>
    <tr>
      <th>4</th>
      <td>12+</td>
      <td>79.99</td>
      <td>14.0</td>
      <td>744.0</td>
      <td>3.2</td>
      <td>Recreate the Solomon R. Guggenheim Museum® wit...</td>
      <td>21035.0</td>
      <td>Discover the architectural secrets of Frank Ll...</td>
      <td>Challenging</td>
      <td>Solomon R. Guggenheim Museum®</td>
      <td>4.6</td>
      <td>Architecture</td>
      <td>4.1</td>
      <td>US</td>
    </tr>
  </tbody>
</table>
</div>



# Using Dictionaries to Rename Column Values
A common use case of dictionaries is to rename the values in a column. For example, let's say that we wanted to rename the *review_difficulty* naming convention to use a quantitative scale.


```python
# Get previous values
df.review_difficulty.unique()
```




    array(['Average', 'Easy', 'Challenging', 'Very Easy', nan,
           'Very Challenging'], dtype=object)



Notice the `nan` value above which represents *null* or blank values. We could potentially translate these difficulty ratings into a quantitative scale like this:


```python
diff_dict = {'Very Easy' : 1, 'Easy' : 2, 'Average' : 3, 'Challenging' : 4, 'Very Challenging' : 5}
```

We could then create a new column (or update the current column) using that dictionary:


```python
df['Difficulty_Rating'] = df.review_difficulty.map(diff_dict)
df.head() #Preview changes
```




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
      <th>ages</th>
      <th>list_price</th>
      <th>num_reviews</th>
      <th>piece_count</th>
      <th>play_star_rating</th>
      <th>prod_desc</th>
      <th>prod_id</th>
      <th>prod_long_desc</th>
      <th>review_difficulty</th>
      <th>set_name</th>
      <th>star_rating</th>
      <th>theme_name</th>
      <th>val_star_rating</th>
      <th>country</th>
      <th>Difficulty_Rating</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>6-12</td>
      <td>29.99</td>
      <td>2.0</td>
      <td>277.0</td>
      <td>4.0</td>
      <td>Catapult into action and take back the eggs fr...</td>
      <td>75823.0</td>
      <td>Use the staircase catapult to launch Red into ...</td>
      <td>Average</td>
      <td>Bird Island Egg Heist</td>
      <td>4.5</td>
      <td>Angry Birds™</td>
      <td>4.0</td>
      <td>US</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>6-12</td>
      <td>19.99</td>
      <td>2.0</td>
      <td>168.0</td>
      <td>4.0</td>
      <td>Launch a flying attack and rescue the eggs fro...</td>
      <td>75822.0</td>
      <td>Pilot Pig has taken off from Bird Island with ...</td>
      <td>Easy</td>
      <td>Piggy Plane Attack</td>
      <td>5.0</td>
      <td>Angry Birds™</td>
      <td>4.0</td>
      <td>US</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>6-12</td>
      <td>12.99</td>
      <td>11.0</td>
      <td>74.0</td>
      <td>4.3</td>
      <td>Chase the piggy with lightning-fast Chuck and ...</td>
      <td>75821.0</td>
      <td>Pitch speedy bird Chuck against the Piggy Car....</td>
      <td>Easy</td>
      <td>Piggy Car Escape</td>
      <td>4.3</td>
      <td>Angry Birds™</td>
      <td>4.1</td>
      <td>US</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>12+</td>
      <td>99.99</td>
      <td>23.0</td>
      <td>1032.0</td>
      <td>3.6</td>
      <td>Explore the architecture of the United States ...</td>
      <td>21030.0</td>
      <td>Discover the architectural secrets of the icon...</td>
      <td>Average</td>
      <td>United States Capitol Building</td>
      <td>4.6</td>
      <td>Architecture</td>
      <td>4.3</td>
      <td>US</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>12+</td>
      <td>79.99</td>
      <td>14.0</td>
      <td>744.0</td>
      <td>3.2</td>
      <td>Recreate the Solomon R. Guggenheim Museum® wit...</td>
      <td>21035.0</td>
      <td>Discover the architectural secrets of Frank Ll...</td>
      <td>Challenging</td>
      <td>Solomon R. Guggenheim Museum®</td>
      <td>4.6</td>
      <td>Architecture</td>
      <td>4.1</td>
      <td>US</td>
      <td>4.0</td>
    </tr>
  </tbody>
</table>
</div>



# Creating Dictionaries from DataFrames
You can also quickly create dictionaries from another dataset. Let's say we want the full name of countries listed under the country column.


```python
df.country.value_counts()[:5]
```




    US    817
    CA    815
    GB    576
    NL    576
    DN    575
    Name: country, dtype: int64




```python
#Pull in a new dataset from online
countries = pd.read_csv('Country_Codes.csv')
countries.head()
```




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
      <th>COUNTRY</th>
      <th>A2 (ISO)</th>
      <th>A3 (UN)</th>
      <th>NUM (UN)</th>
      <th>DIALING CODE</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Afghanistan</td>
      <td>AF</td>
      <td>AFG</td>
      <td>4</td>
      <td>93</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Albania</td>
      <td>AL</td>
      <td>ALB</td>
      <td>8</td>
      <td>355</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Algeria</td>
      <td>DZ</td>
      <td>DZA</td>
      <td>12</td>
      <td>213</td>
    </tr>
    <tr>
      <th>3</th>
      <td>American Samoa</td>
      <td>AS</td>
      <td>ASM</td>
      <td>16</td>
      <td>01/01/84</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Andorra</td>
      <td>AD</td>
      <td>AND</td>
      <td>20</td>
      <td>376</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Create a dictionary
#The zip method is a neat little tool for pairing each entry from two columns together (like a zipper!)
#We then just wrap that in the dict() function.
country_dict = dict(zip(countries['A2 (ISO)'], countries['COUNTRY'])) 
```


```python
#Map it to our original dataset (you can also do this with pd.merge() for joining multiple fields
df['Country_Full_Name'] = df.country.map(country_dict)
df.head(2)
```




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
      <th>ages</th>
      <th>list_price</th>
      <th>num_reviews</th>
      <th>piece_count</th>
      <th>play_star_rating</th>
      <th>prod_desc</th>
      <th>prod_id</th>
      <th>prod_long_desc</th>
      <th>review_difficulty</th>
      <th>set_name</th>
      <th>star_rating</th>
      <th>theme_name</th>
      <th>val_star_rating</th>
      <th>country</th>
      <th>Difficulty_Rating</th>
      <th>Country_Full_Name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>6-12</td>
      <td>29.99</td>
      <td>2.0</td>
      <td>277.0</td>
      <td>4.0</td>
      <td>Catapult into action and take back the eggs fr...</td>
      <td>75823.0</td>
      <td>Use the staircase catapult to launch Red into ...</td>
      <td>Average</td>
      <td>Bird Island Egg Heist</td>
      <td>4.5</td>
      <td>Angry Birds™</td>
      <td>4.0</td>
      <td>US</td>
      <td>3.0</td>
      <td>United States</td>
    </tr>
    <tr>
      <th>1</th>
      <td>6-12</td>
      <td>19.99</td>
      <td>2.0</td>
      <td>168.0</td>
      <td>4.0</td>
      <td>Launch a flying attack and rescue the eggs fro...</td>
      <td>75822.0</td>
      <td>Pilot Pig has taken off from Bird Island with ...</td>
      <td>Easy</td>
      <td>Piggy Plane Attack</td>
      <td>5.0</td>
      <td>Angry Birds™</td>
      <td>4.0</td>
      <td>US</td>
      <td>2.0</td>
      <td>United States</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.Country_Full_Name.value_counts()[:5]
```




    United States     817
    Canada            815
    Netherlands       576
    United Kingdom    576
    Austria           575
    Name: Country_Full_Name, dtype: int64



# Custom Agg Functions
We can also use dictionaries along with the pandas groupby method to apply different aggregations to different columns:


```python
import numpy as np
```


```python
agg_dict = {'ages' : 'max',
            'Difficulty_Rating' : [np.mean, np.std],
           'Country_Full_Name' : lambda x: x.value_counts().index[0],
           'num_reviews' : ['mean', 'max']}
df.groupby('theme_name').agg(agg_dict)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th>ages</th>
      <th colspan="2" halign="left">Difficulty_Rating</th>
      <th>Country_Full_Name</th>
      <th colspan="2" halign="left">num_reviews</th>
    </tr>
    <tr>
      <th></th>
      <th>max</th>
      <th>mean</th>
      <th>std</th>
      <th>&lt;lambda&gt;</th>
      <th>mean</th>
      <th>max</th>
    </tr>
    <tr>
      <th>theme_name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Angry Birds™</th>
      <td>6-12</td>
      <td>2.333333</td>
      <td>0.516398</td>
      <td>United States</td>
      <td>5.000000</td>
      <td>11.0</td>
    </tr>
    <tr>
      <th>Architecture</th>
      <td>12+</td>
      <td>3.000000</td>
      <td>0.448282</td>
      <td>Finland</td>
      <td>21.300000</td>
      <td>53.0</td>
    </tr>
    <tr>
      <th>BOOST</th>
      <td>7-12</td>
      <td>3.000000</td>
      <td>0.000000</td>
      <td>Finland</td>
      <td>63.000000</td>
      <td>63.0</td>
    </tr>
    <tr>
      <th>Blue's Helicopter Pursuit</th>
      <td>7-12</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Finland</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>BrickHeadz</th>
      <td>10+</td>
      <td>1.782673</td>
      <td>0.606140</td>
      <td>Canada</td>
      <td>3.219917</td>
      <td>14.0</td>
    </tr>
    <tr>
      <th>Carnotaurus Gyrosphere Escape</th>
      <td>7-12</td>
      <td>3.000000</td>
      <td>0.000000</td>
      <td>Finland</td>
      <td>1.714286</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>City</th>
      <td>8-12</td>
      <td>2.166335</td>
      <td>0.755981</td>
      <td>Canada</td>
      <td>12.892176</td>
      <td>89.0</td>
    </tr>
    <tr>
      <th>Classic</th>
      <td>4-99</td>
      <td>1.700680</td>
      <td>0.695328</td>
      <td>New Zealand</td>
      <td>21.054313</td>
      <td>180.0</td>
    </tr>
    <tr>
      <th>Creator 3-in-1</th>
      <td>9-14</td>
      <td>2.511811</td>
      <td>0.500518</td>
      <td>United States</td>
      <td>7.842520</td>
      <td>27.0</td>
    </tr>
    <tr>
      <th>Creator Expert</th>
      <td>16+</td>
      <td>3.728707</td>
      <td>0.445330</td>
      <td>Canada</td>
      <td>123.526814</td>
      <td>337.0</td>
    </tr>
    <tr>
      <th>DC Comics™ Super Heroes</th>
      <td>9-14</td>
      <td>2.621622</td>
      <td>0.486629</td>
      <td>Canada</td>
      <td>7.945946</td>
      <td>47.0</td>
    </tr>
    <tr>
      <th>DC Super Hero Girls</th>
      <td>9-12</td>
      <td>2.833333</td>
      <td>0.380693</td>
      <td>United States</td>
      <td>3.000000</td>
      <td>7.0</td>
    </tr>
    <tr>
      <th>DIMENSIONS™</th>
      <td>7-14</td>
      <td>2.195312</td>
      <td>0.501896</td>
      <td>Netherlands</td>
      <td>3.929688</td>
      <td>13.0</td>
    </tr>
    <tr>
      <th>DUPLO®</th>
      <td>2-5</td>
      <td>2.066798</td>
      <td>0.717784</td>
      <td>Canada</td>
      <td>4.117133</td>
      <td>22.0</td>
    </tr>
    <tr>
      <th>Dilophosaurus Outpost Attack</th>
      <td>7-12</td>
      <td>2.000000</td>
      <td>0.000000</td>
      <td>Finland</td>
      <td>1.809524</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>Disney™</th>
      <td>6-12</td>
      <td>2.815385</td>
      <td>0.711566</td>
      <td>Canada</td>
      <td>20.234615</td>
      <td>171.0</td>
    </tr>
    <tr>
      <th>Elves</th>
      <td>9-12</td>
      <td>2.849673</td>
      <td>0.358565</td>
      <td>Canada</td>
      <td>3.010256</td>
      <td>8.0</td>
    </tr>
    <tr>
      <th>Friends</th>
      <td>8-12</td>
      <td>2.808853</td>
      <td>0.636334</td>
      <td>Canada</td>
      <td>3.904031</td>
      <td>18.0</td>
    </tr>
    <tr>
      <th>Ghostbusters™</th>
      <td>8-14</td>
      <td>3.913043</td>
      <td>0.288104</td>
      <td>Canada</td>
      <td>120.782609</td>
      <td>130.0</td>
    </tr>
    <tr>
      <th>Ideas</th>
      <td>9+</td>
      <td>2.671875</td>
      <td>0.743575</td>
      <td>Canada</td>
      <td>101.757812</td>
      <td>367.0</td>
    </tr>
    <tr>
      <th>Indoraptor Rampage at Lockwood Estate</th>
      <td>8-12</td>
      <td>2.000000</td>
      <td>0.000000</td>
      <td>Finland</td>
      <td>2.952381</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>Juniors</th>
      <td>5-8</td>
      <td>2.058932</td>
      <td>0.751523</td>
      <td>Canada</td>
      <td>2.283951</td>
      <td>8.0</td>
    </tr>
    <tr>
      <th>Jurassic Park Velociraptor Chase</th>
      <td>6-12</td>
      <td>3.000000</td>
      <td>0.000000</td>
      <td>Finland</td>
      <td>4.000000</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>LEGO® Creator 3-in-1</th>
      <td>8-12</td>
      <td>2.533333</td>
      <td>0.516398</td>
      <td>Canada</td>
      <td>4.666667</td>
      <td>15.0</td>
    </tr>
    <tr>
      <th>MINDSTORMS®</th>
      <td>8+</td>
      <td>2.377246</td>
      <td>1.225319</td>
      <td>France</td>
      <td>6.648936</td>
      <td>38.0</td>
    </tr>
    <tr>
      <th>Marvel Super Heroes</th>
      <td>8-14</td>
      <td>2.389785</td>
      <td>0.520422</td>
      <td>United States</td>
      <td>11.919355</td>
      <td>54.0</td>
    </tr>
    <tr>
      <th>Minecraft™</th>
      <td>8+</td>
      <td>2.754789</td>
      <td>0.713352</td>
      <td>Canada</td>
      <td>5.544061</td>
      <td>16.0</td>
    </tr>
    <tr>
      <th>Minifigures</th>
      <td>5+</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>Canada</td>
      <td>14.785714</td>
      <td>26.0</td>
    </tr>
    <tr>
      <th>NEXO KNIGHTS™</th>
      <td>9-14</td>
      <td>3.008621</td>
      <td>0.982417</td>
      <td>Canada</td>
      <td>2.950820</td>
      <td>17.0</td>
    </tr>
    <tr>
      <th>NINJAGO®</th>
      <td>9-14</td>
      <td>2.849162</td>
      <td>0.902330</td>
      <td>Canada</td>
      <td>9.513966</td>
      <td>61.0</td>
    </tr>
    <tr>
      <th>Power Functions</th>
      <td>9-16</td>
      <td>2.000000</td>
      <td>0.000000</td>
      <td>Finland</td>
      <td>57.000000</td>
      <td>57.0</td>
    </tr>
    <tr>
      <th>Pteranodon Chase</th>
      <td>6-12</td>
      <td>2.476190</td>
      <td>0.511766</td>
      <td>Finland</td>
      <td>2.238095</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>SERIOUS PLAY®</th>
      <td>6+</td>
      <td>2.250000</td>
      <td>0.435613</td>
      <td>Finland</td>
      <td>6.750000</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>Speed Champions</th>
      <td>8-14</td>
      <td>2.338583</td>
      <td>0.474162</td>
      <td>Canada</td>
      <td>8.968504</td>
      <td>28.0</td>
    </tr>
    <tr>
      <th>Star Wars™</th>
      <td>9-14</td>
      <td>2.441755</td>
      <td>0.883020</td>
      <td>United States</td>
      <td>25.908472</td>
      <td>201.0</td>
    </tr>
    <tr>
      <th>Stygimoloch Breakout</th>
      <td>6-12</td>
      <td>3.000000</td>
      <td>0.000000</td>
      <td>Finland</td>
      <td>2.000000</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>T. rex Transport</th>
      <td>7-12</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Finland</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>THE LEGO® BATMAN MOVIE</th>
      <td>9-14</td>
      <td>2.773469</td>
      <td>0.596265</td>
      <td>Canada</td>
      <td>12.312030</td>
      <td>27.0</td>
    </tr>
    <tr>
      <th>THE LEGO® NINJAGO® MOVIE™</th>
      <td>9-14</td>
      <td>2.739623</td>
      <td>0.712520</td>
      <td>Australia</td>
      <td>17.665409</td>
      <td>88.0</td>
    </tr>
    <tr>
      <th>Technic</th>
      <td>9-16</td>
      <td>2.869835</td>
      <td>0.809876</td>
      <td>Canada</td>
      <td>18.768317</td>
      <td>143.0</td>
    </tr>
  </tbody>
</table>
</div>



# Data Transformation

Create a dictionary that rebins the age column to the following age ranges:
Under 5, 5-8, 8-12, 12+

*If there is a conflict in age bin, default to the higher age bin.


```python
# Your code here
```

# Data Visualization
Create a bar graph depicting the number of lego sets for the original age range column. Then create a second bar graph for the new age column you created. How do they compare?


```python
# Your code here
```
