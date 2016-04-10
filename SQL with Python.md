

```python
from IPython.display import Image
Image(url='http://www.dbquanti.eu/css/images/database.png')

```




<img src="http://www.dbquanti.eu/css/images/database.png"/>




```python
import sqlite3
import pandas as pd
```


```python
#Connect to the database (We've downloaded the sakila database)
con = sqlite3.connect('sakila.db')
```


```python
#Set function as our sql_to_pandas DataFrame

def sql_to_df(sql_query): 
    df = pd.read_sql(sql_query, con) #Use pandas to pass the SQL query using the connection from SQLite3
    return df  #return the DataFrame
```

### Selecting multiple columns


```python
query = '''SELECT first_name, last_name FROM customer;'''
sql_to_df(query).head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>first_name</th>
      <th>last_name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>MARY</td>
      <td>SMITH</td>
    </tr>
    <tr>
      <th>1</th>
      <td>PATRICIA</td>
      <td>JOHNSON</td>
    </tr>
    <tr>
      <th>2</th>
      <td>LINDA</td>
      <td>WILLIAMS</td>
    </tr>
    <tr>
      <th>3</th>
      <td>BARBARA</td>
      <td>JONES</td>
    </tr>
    <tr>
      <th>4</th>
      <td>ELIZABETH</td>
      <td>BROWN</td>
    </tr>
  </tbody>
</table>
</div>



### Selecting everything from the table


```python
query = '''SELECT * FROM customer;''' #select everything from the customer table
sql_to_df(query).head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>customer_id</th>
      <th>store_id</th>
      <th>first_name</th>
      <th>last_name</th>
      <th>email</th>
      <th>address_id</th>
      <th>active</th>
      <th>create_date</th>
      <th>last_update</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>MARY</td>
      <td>SMITH</td>
      <td>MARY.SMITH@sakilacustomer.org</td>
      <td>5</td>
      <td>1</td>
      <td>2006-02-14 22:04:36.000</td>
      <td>2011-09-14 18:10:28</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>PATRICIA</td>
      <td>JOHNSON</td>
      <td>PATRICIA.JOHNSON@sakilacustomer.org</td>
      <td>6</td>
      <td>1</td>
      <td>2006-02-14 22:04:36.000</td>
      <td>2011-09-14 18:10:28</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>LINDA</td>
      <td>WILLIAMS</td>
      <td>LINDA.WILLIAMS@sakilacustomer.org</td>
      <td>7</td>
      <td>1</td>
      <td>2006-02-14 22:04:36.000</td>
      <td>2011-09-14 18:10:28</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>2</td>
      <td>BARBARA</td>
      <td>JONES</td>
      <td>BARBARA.JONES@sakilacustomer.org</td>
      <td>8</td>
      <td>1</td>
      <td>2006-02-14 22:04:36.000</td>
      <td>2011-09-14 18:10:28</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>1</td>
      <td>ELIZABETH</td>
      <td>BROWN</td>
      <td>ELIZABETH.BROWN@sakilacustomer.org</td>
      <td>9</td>
      <td>1</td>
      <td>2006-02-14 22:04:36.000</td>
      <td>2011-09-14 18:10:28</td>
    </tr>
  </tbody>
</table>
</div>



### Select distinct values


```python
query = '''SELECT DISTINCT country_id FROM city'''
pd.read_sql(query,con).head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>country_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>




```python
query = '''SELECT DISTINCT store_id FROM staff;'''
pd.read_sql(query,con)
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>store_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>



### Syntax for SQL WHERE
The WHERE clause is used for filtering records
SELECT column_name
FROM table_name
WHERE column_name (math operator) desired_value

```python
#Select all customer information from all but the 1st store
query = '''SELECT * 
        FROM customer
        WHERE store_id != 1;'''

pd.read_sql(query,con).head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>customer_id</th>
      <th>store_id</th>
      <th>first_name</th>
      <th>last_name</th>
      <th>email</th>
      <th>address_id</th>
      <th>active</th>
      <th>create_date</th>
      <th>last_update</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>4</td>
      <td>2</td>
      <td>BARBARA</td>
      <td>JONES</td>
      <td>BARBARA.JONES@sakilacustomer.org</td>
      <td>8</td>
      <td>1</td>
      <td>2006-02-14 22:04:36.000</td>
      <td>2011-09-14 18:10:28</td>
    </tr>
    <tr>
      <th>1</th>
      <td>6</td>
      <td>2</td>
      <td>JENNIFER</td>
      <td>DAVIS</td>
      <td>JENNIFER.DAVIS@sakilacustomer.org</td>
      <td>10</td>
      <td>1</td>
      <td>2006-02-14 22:04:36.000</td>
      <td>2011-09-14 18:10:28</td>
    </tr>
    <tr>
      <th>2</th>
      <td>8</td>
      <td>2</td>
      <td>SUSAN</td>
      <td>WILSON</td>
      <td>SUSAN.WILSON@sakilacustomer.org</td>
      <td>12</td>
      <td>1</td>
      <td>2006-02-14 22:04:36.000</td>
      <td>2011-09-14 18:10:28</td>
    </tr>
    <tr>
      <th>3</th>
      <td>9</td>
      <td>2</td>
      <td>MARGARET</td>
      <td>MOORE</td>
      <td>MARGARET.MOORE@sakilacustomer.org</td>
      <td>13</td>
      <td>1</td>
      <td>2006-02-14 22:04:36.000</td>
      <td>2011-09-14 18:10:28</td>
    </tr>
    <tr>
      <th>4</th>
      <td>11</td>
      <td>2</td>
      <td>LISA</td>
      <td>ANDERSON</td>
      <td>LISA.ANDERSON@sakilacustomer.org</td>
      <td>15</td>
      <td>1</td>
      <td>2006-02-14 22:04:36.000</td>
      <td>2011-09-14 18:10:28</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Select all of Mary's customer info
query = '''SELECT * FROM customer
            WHERE first_name = 'MARY' '''
pd.read_sql(query,con)
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>customer_id</th>
      <th>store_id</th>
      <th>first_name</th>
      <th>last_name</th>
      <th>email</th>
      <th>address_id</th>
      <th>active</th>
      <th>create_date</th>
      <th>last_update</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>MARY</td>
      <td>SMITH</td>
      <td>MARY.SMITH@sakilacustomer.org</td>
      <td>5</td>
      <td>1</td>
      <td>2006-02-14 22:04:36.000</td>
      <td>2011-09-14 18:10:28</td>
    </tr>
  </tbody>
</table>
</div>



### AND and OR opreators


```python
query = '''SELECT * FROM film
            WHERE release_year = 2006
            AND rating = 'R' '''
pd.read_sql(query,con).head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>film_id</th>
      <th>title</th>
      <th>description</th>
      <th>release_year</th>
      <th>language_id</th>
      <th>original_language_id</th>
      <th>rental_duration</th>
      <th>rental_rate</th>
      <th>length</th>
      <th>replacement_cost</th>
      <th>rating</th>
      <th>special_features</th>
      <th>last_update</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>8</td>
      <td>AIRPORT POLLOCK</td>
      <td>A Epic Tale of a Moose And a Girl who must Con...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>6</td>
      <td>4.99</td>
      <td>54</td>
      <td>15.99</td>
      <td>R</td>
      <td>Trailers</td>
      <td>2011-09-14 18:05:33</td>
    </tr>
    <tr>
      <th>1</th>
      <td>17</td>
      <td>ALONE TRIP</td>
      <td>A Fast-Paced Character Study of a Composer And...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>3</td>
      <td>0.99</td>
      <td>82</td>
      <td>14.99</td>
      <td>R</td>
      <td>Trailers,Behind the Scenes</td>
      <td>2011-09-14 18:05:33</td>
    </tr>
    <tr>
      <th>2</th>
      <td>20</td>
      <td>AMELIE HELLFIGHTERS</td>
      <td>A Boring Drama of a Woman And a Squirrel who m...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>4</td>
      <td>4.99</td>
      <td>79</td>
      <td>23.99</td>
      <td>R</td>
      <td>Commentaries,Deleted Scenes,Behind the Scenes</td>
      <td>2011-09-14 18:05:33</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>AMERICAN CIRCUS</td>
      <td>A Insightful Drama of a Girl And a Astronaut w...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>3</td>
      <td>4.99</td>
      <td>129</td>
      <td>17.99</td>
      <td>R</td>
      <td>Commentaries,Behind the Scenes</td>
      <td>2011-09-14 18:05:33</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>ANACONDA CONFESSIONS</td>
      <td>A Lacklusture Display of a Dentist And a Denti...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>3</td>
      <td>0.99</td>
      <td>92</td>
      <td>9.99</td>
      <td>R</td>
      <td>Trailers,Deleted Scenes</td>
      <td>2011-09-14 18:05:33</td>
    </tr>
  </tbody>
</table>
</div>




```python
query = '''SELECT * FROM film
            WHERE rating = 'PG'
            OR rating = 'R';
        '''
pd.read_sql(query,con)
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>film_id</th>
      <th>title</th>
      <th>description</th>
      <th>release_year</th>
      <th>language_id</th>
      <th>original_language_id</th>
      <th>rental_duration</th>
      <th>rental_rate</th>
      <th>length</th>
      <th>replacement_cost</th>
      <th>rating</th>
      <th>special_features</th>
      <th>last_update</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>ACADEMY DINOSAUR</td>
      <td>A Epic Drama of a Feminist And a Mad Scientist...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>6</td>
      <td>0.99</td>
      <td>86</td>
      <td>20.99</td>
      <td>PG</td>
      <td>Deleted Scenes,Behind the Scenes</td>
      <td>2011-09-14 18:05:32</td>
    </tr>
    <tr>
      <th>1</th>
      <td>6</td>
      <td>AGENT TRUMAN</td>
      <td>A Intrepid Panorama of a Robot And a Boy who m...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>3</td>
      <td>2.99</td>
      <td>169</td>
      <td>17.99</td>
      <td>PG</td>
      <td>Deleted Scenes</td>
      <td>2011-09-14 18:05:33</td>
    </tr>
    <tr>
      <th>2</th>
      <td>8</td>
      <td>AIRPORT POLLOCK</td>
      <td>A Epic Tale of a Moose And a Girl who must Con...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>6</td>
      <td>4.99</td>
      <td>54</td>
      <td>15.99</td>
      <td>R</td>
      <td>Trailers</td>
      <td>2011-09-14 18:05:33</td>
    </tr>
    <tr>
      <th>3</th>
      <td>12</td>
      <td>ALASKA PHANTOM</td>
      <td>A Fanciful Saga of a Hunter And a Pastry Chef ...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>6</td>
      <td>0.99</td>
      <td>136</td>
      <td>22.99</td>
      <td>PG</td>
      <td>Commentaries,Deleted Scenes</td>
      <td>2011-09-14 18:05:33</td>
    </tr>
    <tr>
      <th>4</th>
      <td>13</td>
      <td>ALI FOREVER</td>
      <td>A Action-Packed Drama of a Dentist And a Croco...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>4</td>
      <td>4.99</td>
      <td>150</td>
      <td>21.99</td>
      <td>PG</td>
      <td>Deleted Scenes,Behind the Scenes</td>
      <td>2011-09-14 18:05:33</td>
    </tr>
    <tr>
      <th>5</th>
      <td>17</td>
      <td>ALONE TRIP</td>
      <td>A Fast-Paced Character Study of a Composer And...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>3</td>
      <td>0.99</td>
      <td>82</td>
      <td>14.99</td>
      <td>R</td>
      <td>Trailers,Behind the Scenes</td>
      <td>2011-09-14 18:05:33</td>
    </tr>
    <tr>
      <th>6</th>
      <td>19</td>
      <td>AMADEUS HOLY</td>
      <td>A Emotional Display of a Pioneer And a Technic...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>6</td>
      <td>0.99</td>
      <td>113</td>
      <td>20.99</td>
      <td>PG</td>
      <td>Commentaries,Deleted Scenes,Behind the Scenes</td>
      <td>2011-09-14 18:05:33</td>
    </tr>
    <tr>
      <th>7</th>
      <td>20</td>
      <td>AMELIE HELLFIGHTERS</td>
      <td>A Boring Drama of a Woman And a Squirrel who m...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>4</td>
      <td>4.99</td>
      <td>79</td>
      <td>23.99</td>
      <td>R</td>
      <td>Commentaries,Deleted Scenes,Behind the Scenes</td>
      <td>2011-09-14 18:05:33</td>
    </tr>
    <tr>
      <th>8</th>
      <td>21</td>
      <td>AMERICAN CIRCUS</td>
      <td>A Insightful Drama of a Girl And a Astronaut w...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>3</td>
      <td>4.99</td>
      <td>129</td>
      <td>17.99</td>
      <td>R</td>
      <td>Commentaries,Behind the Scenes</td>
      <td>2011-09-14 18:05:33</td>
    </tr>
    <tr>
      <th>9</th>
      <td>23</td>
      <td>ANACONDA CONFESSIONS</td>
      <td>A Lacklusture Display of a Dentist And a Denti...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>3</td>
      <td>0.99</td>
      <td>92</td>
      <td>9.99</td>
      <td>R</td>
      <td>Trailers,Deleted Scenes</td>
      <td>2011-09-14 18:05:33</td>
    </tr>
    <tr>
      <th>10</th>
      <td>24</td>
      <td>ANALYZE HOOSIERS</td>
      <td>A Thoughtful Display of a Explorer And a Pastr...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>6</td>
      <td>2.99</td>
      <td>181</td>
      <td>19.99</td>
      <td>R</td>
      <td>Trailers,Behind the Scenes</td>
      <td>2011-09-14 18:05:33</td>
    </tr>
    <tr>
      <th>11</th>
      <td>30</td>
      <td>ANYTHING SAVANNAH</td>
      <td>A Epic Story of a Pastry Chef And a Woman who ...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>4</td>
      <td>2.99</td>
      <td>82</td>
      <td>27.99</td>
      <td>R</td>
      <td>Trailers,Deleted Scenes,Behind the Scenes</td>
      <td>2011-09-14 18:05:33</td>
    </tr>
    <tr>
      <th>12</th>
      <td>32</td>
      <td>APOCALYPSE FLAMINGOS</td>
      <td>A Astounding Story of a Dog And a Squirrel who...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>6</td>
      <td>4.99</td>
      <td>119</td>
      <td>11.99</td>
      <td>R</td>
      <td>Trailers,Commentaries</td>
      <td>2011-09-14 18:05:33</td>
    </tr>
    <tr>
      <th>13</th>
      <td>37</td>
      <td>ARIZONA BANG</td>
      <td>A Brilliant Panorama of a Mad Scientist And a ...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>3</td>
      <td>2.99</td>
      <td>121</td>
      <td>28.99</td>
      <td>PG</td>
      <td>Trailers,Deleted Scenes</td>
      <td>2011-09-14 18:05:33</td>
    </tr>
    <tr>
      <th>14</th>
      <td>40</td>
      <td>ARMY FLINTSTONES</td>
      <td>A Boring Saga of a Database Administrator And ...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>4</td>
      <td>0.99</td>
      <td>148</td>
      <td>22.99</td>
      <td>R</td>
      <td>Trailers,Commentaries</td>
      <td>2011-09-14 18:05:33</td>
    </tr>
    <tr>
      <th>15</th>
      <td>41</td>
      <td>ARSENIC INDEPENDENCE</td>
      <td>A Fanciful Documentary of a Mad Cow And a Woma...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>4</td>
      <td>0.99</td>
      <td>137</td>
      <td>17.99</td>
      <td>PG</td>
      <td>Trailers,Deleted Scenes,Behind the Scenes</td>
      <td>2011-09-14 18:05:33</td>
    </tr>
    <tr>
      <th>16</th>
      <td>49</td>
      <td>BADMAN DAWN</td>
      <td>A Emotional Panorama of a Pioneer And a Compos...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>6</td>
      <td>2.99</td>
      <td>162</td>
      <td>22.99</td>
      <td>R</td>
      <td>Trailers,Commentaries,Behind the Scenes</td>
      <td>2011-09-14 18:05:33</td>
    </tr>
    <tr>
      <th>17</th>
      <td>54</td>
      <td>BANGER PINOCCHIO</td>
      <td>A Awe-Inspiring Drama of a Car And a Pastry Ch...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>5</td>
      <td>0.99</td>
      <td>113</td>
      <td>15.99</td>
      <td>R</td>
      <td>Trailers,Commentaries,Deleted Scenes</td>
      <td>2011-09-14 18:05:34</td>
    </tr>
    <tr>
      <th>18</th>
      <td>59</td>
      <td>BEAR GRACELAND</td>
      <td>A Astounding Saga of a Dog And a Boy who must ...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>4</td>
      <td>2.99</td>
      <td>160</td>
      <td>20.99</td>
      <td>R</td>
      <td>Deleted Scenes</td>
      <td>2011-09-14 18:05:34</td>
    </tr>
    <tr>
      <th>19</th>
      <td>60</td>
      <td>BEAST HUNCHBACK</td>
      <td>A Awe-Inspiring Epistle of a Student And a Squ...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>3</td>
      <td>4.99</td>
      <td>89</td>
      <td>22.99</td>
      <td>R</td>
      <td>Deleted Scenes,Behind the Scenes</td>
      <td>2011-09-14 18:05:34</td>
    </tr>
    <tr>
      <th>20</th>
      <td>63</td>
      <td>BEDAZZLED MARRIED</td>
      <td>A Astounding Character Study of a Madman And a...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>6</td>
      <td>0.99</td>
      <td>73</td>
      <td>21.99</td>
      <td>PG</td>
      <td>Trailers,Deleted Scenes,Behind the Scenes</td>
      <td>2011-09-14 18:05:34</td>
    </tr>
    <tr>
      <th>21</th>
      <td>65</td>
      <td>BEHAVIOR RUNAWAY</td>
      <td>A Unbelieveable Drama of a Student And a Husba...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>3</td>
      <td>4.99</td>
      <td>100</td>
      <td>20.99</td>
      <td>PG</td>
      <td>Trailers,Deleted Scenes,Behind the Scenes</td>
      <td>2011-09-14 18:05:34</td>
    </tr>
    <tr>
      <th>22</th>
      <td>69</td>
      <td>BEVERLY OUTLAW</td>
      <td>A Fanciful Documentary of a Womanizer And a Bo...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>3</td>
      <td>2.99</td>
      <td>85</td>
      <td>21.99</td>
      <td>R</td>
      <td>Trailers</td>
      <td>2011-09-14 18:05:34</td>
    </tr>
    <tr>
      <th>23</th>
      <td>72</td>
      <td>BILL OTHERS</td>
      <td>A Stunning Saga of a Mad Scientist And a Foren...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>6</td>
      <td>2.99</td>
      <td>93</td>
      <td>12.99</td>
      <td>PG</td>
      <td>Trailers,Commentaries</td>
      <td>2011-09-14 18:05:34</td>
    </tr>
    <tr>
      <th>24</th>
      <td>74</td>
      <td>BIRCH ANTITRUST</td>
      <td>A Fanciful Panorama of a Husband And a Pioneer...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>4</td>
      <td>4.99</td>
      <td>162</td>
      <td>18.99</td>
      <td>PG</td>
      <td>Trailers,Commentaries,Deleted Scenes</td>
      <td>2011-09-14 18:05:34</td>
    </tr>
    <tr>
      <th>25</th>
      <td>78</td>
      <td>BLACKOUT PRIVATE</td>
      <td>A Intrepid Yarn of a Pastry Chef And a Mad Sci...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>7</td>
      <td>2.99</td>
      <td>85</td>
      <td>12.99</td>
      <td>PG</td>
      <td>Trailers,Deleted Scenes</td>
      <td>2011-09-14 18:05:34</td>
    </tr>
    <tr>
      <th>26</th>
      <td>84</td>
      <td>BOILED DARES</td>
      <td>A Awe-Inspiring Story of a Waitress And a Dog ...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>7</td>
      <td>4.99</td>
      <td>102</td>
      <td>13.99</td>
      <td>PG</td>
      <td>Trailers,Commentaries</td>
      <td>2011-09-14 18:05:34</td>
    </tr>
    <tr>
      <th>27</th>
      <td>86</td>
      <td>BOOGIE AMELIE</td>
      <td>A Lacklusture Character Study of a Husband And...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>6</td>
      <td>4.99</td>
      <td>121</td>
      <td>11.99</td>
      <td>R</td>
      <td>Commentaries,Behind the Scenes</td>
      <td>2011-09-14 18:05:34</td>
    </tr>
    <tr>
      <th>28</th>
      <td>88</td>
      <td>BORN SPINAL</td>
      <td>A Touching Epistle of a Frisbee And a Husband ...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>7</td>
      <td>4.99</td>
      <td>179</td>
      <td>17.99</td>
      <td>PG</td>
      <td>Trailers,Commentaries,Deleted Scenes</td>
      <td>2011-09-14 18:05:34</td>
    </tr>
    <tr>
      <th>29</th>
      <td>90</td>
      <td>BOULEVARD MOB</td>
      <td>A Fateful Epistle of a Moose And a Monkey who ...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>3</td>
      <td>0.99</td>
      <td>63</td>
      <td>11.99</td>
      <td>R</td>
      <td>Trailers</td>
      <td>2011-09-14 18:05:34</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>359</th>
      <td>925</td>
      <td>UNITED PILOT</td>
      <td>A Fast-Paced Reflection of a Cat And a Mad Cow...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>3</td>
      <td>0.99</td>
      <td>164</td>
      <td>27.99</td>
      <td>R</td>
      <td>Trailers,Deleted Scenes</td>
      <td>2011-09-14 18:05:54</td>
    </tr>
    <tr>
      <th>360</th>
      <td>928</td>
      <td>UPTOWN YOUNG</td>
      <td>A Fateful Documentary of a Dog And a Hunter wh...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>5</td>
      <td>2.99</td>
      <td>84</td>
      <td>16.99</td>
      <td>PG</td>
      <td>Commentaries</td>
      <td>2011-09-14 18:05:54</td>
    </tr>
    <tr>
      <th>361</th>
      <td>930</td>
      <td>VACATION BOONDOCK</td>
      <td>A Fanciful Character Study of a Secret Agent A...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>4</td>
      <td>2.99</td>
      <td>145</td>
      <td>23.99</td>
      <td>R</td>
      <td>Commentaries</td>
      <td>2011-09-14 18:05:54</td>
    </tr>
    <tr>
      <th>362</th>
      <td>935</td>
      <td>VANISHED GARDEN</td>
      <td>A Intrepid Character Study of a Squirrel And a...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>5</td>
      <td>0.99</td>
      <td>142</td>
      <td>17.99</td>
      <td>R</td>
      <td>Trailers,Commentaries,Deleted Scenes</td>
      <td>2011-09-14 18:05:54</td>
    </tr>
    <tr>
      <th>363</th>
      <td>938</td>
      <td>VELVET TERMINATOR</td>
      <td>A Lacklusture Tale of a Pastry Chef And a Tech...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>3</td>
      <td>4.99</td>
      <td>173</td>
      <td>14.99</td>
      <td>R</td>
      <td>Behind the Scenes</td>
      <td>2011-09-14 18:05:54</td>
    </tr>
    <tr>
      <th>364</th>
      <td>939</td>
      <td>VERTIGO NORTHWEST</td>
      <td>A Unbelieveable Display of a Mad Scientist And...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>4</td>
      <td>2.99</td>
      <td>90</td>
      <td>17.99</td>
      <td>R</td>
      <td>Commentaries,Behind the Scenes</td>
      <td>2011-09-14 18:05:55</td>
    </tr>
    <tr>
      <th>365</th>
      <td>945</td>
      <td>VIRGINIAN PLUTO</td>
      <td>A Emotional Panorama of a Dentist And a Crocod...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>5</td>
      <td>0.99</td>
      <td>164</td>
      <td>22.99</td>
      <td>R</td>
      <td>Deleted Scenes</td>
      <td>2011-09-14 18:05:55</td>
    </tr>
    <tr>
      <th>366</th>
      <td>950</td>
      <td>VOLUME HOUSE</td>
      <td>A Boring Tale of a Dog And a Woman who must Me...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>7</td>
      <td>4.99</td>
      <td>132</td>
      <td>12.99</td>
      <td>PG</td>
      <td>Commentaries</td>
      <td>2011-09-14 18:05:55</td>
    </tr>
    <tr>
      <th>367</th>
      <td>952</td>
      <td>WAGON JAWS</td>
      <td>A Intrepid Drama of a Moose And a Boat who mus...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>7</td>
      <td>2.99</td>
      <td>152</td>
      <td>17.99</td>
      <td>PG</td>
      <td>Deleted Scenes,Behind the Scenes</td>
      <td>2011-09-14 18:05:55</td>
    </tr>
    <tr>
      <th>368</th>
      <td>955</td>
      <td>WALLS ARTIST</td>
      <td>A Insightful Panorama of a Teacher And a Teach...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>7</td>
      <td>4.99</td>
      <td>135</td>
      <td>19.99</td>
      <td>PG</td>
      <td>Trailers,Behind the Scenes</td>
      <td>2011-09-14 18:05:55</td>
    </tr>
    <tr>
      <th>369</th>
      <td>961</td>
      <td>WASH HEAVENLY</td>
      <td>A Awe-Inspiring Reflection of a Cat And a Pion...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>7</td>
      <td>4.99</td>
      <td>161</td>
      <td>22.99</td>
      <td>R</td>
      <td>Commentaries</td>
      <td>2011-09-14 18:05:55</td>
    </tr>
    <tr>
      <th>370</th>
      <td>962</td>
      <td>WASTELAND DIVINE</td>
      <td>A Fanciful Story of a Database Administrator A...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>7</td>
      <td>2.99</td>
      <td>85</td>
      <td>18.99</td>
      <td>PG</td>
      <td>Trailers,Deleted Scenes,Behind the Scenes</td>
      <td>2011-09-14 18:05:55</td>
    </tr>
    <tr>
      <th>371</th>
      <td>963</td>
      <td>WATCH TRACY</td>
      <td>A Fast-Paced Yarn of a Dog And a Frisbee who m...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>5</td>
      <td>0.99</td>
      <td>78</td>
      <td>12.99</td>
      <td>PG</td>
      <td>Trailers,Deleted Scenes,Behind the Scenes</td>
      <td>2011-09-14 18:05:55</td>
    </tr>
    <tr>
      <th>372</th>
      <td>966</td>
      <td>WEDDING APOLLO</td>
      <td>A Action-Packed Tale of a Student And a Waitre...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>3</td>
      <td>0.99</td>
      <td>70</td>
      <td>14.99</td>
      <td>PG</td>
      <td>Trailers</td>
      <td>2011-09-14 18:05:55</td>
    </tr>
    <tr>
      <th>373</th>
      <td>967</td>
      <td>WEEKEND PERSONAL</td>
      <td>A Fast-Paced Documentary of a Car And a Butler...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>5</td>
      <td>2.99</td>
      <td>134</td>
      <td>26.99</td>
      <td>R</td>
      <td>Trailers,Commentaries,Deleted Scenes,Behind th...</td>
      <td>2011-09-14 18:05:55</td>
    </tr>
    <tr>
      <th>374</th>
      <td>974</td>
      <td>WILD APOLLO</td>
      <td>A Beautiful Story of a Monkey And a Sumo Wrest...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>4</td>
      <td>0.99</td>
      <td>181</td>
      <td>24.99</td>
      <td>R</td>
      <td>Trailers,Commentaries,Deleted Scenes,Behind th...</td>
      <td>2011-09-14 18:05:55</td>
    </tr>
    <tr>
      <th>375</th>
      <td>975</td>
      <td>WILLOW TRACY</td>
      <td>A Brilliant Panorama of a Boat And a Astronaut...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>6</td>
      <td>2.99</td>
      <td>137</td>
      <td>22.99</td>
      <td>R</td>
      <td>Trailers,Commentaries,Behind the Scenes</td>
      <td>2011-09-14 18:05:55</td>
    </tr>
    <tr>
      <th>376</th>
      <td>976</td>
      <td>WIND PHANTOM</td>
      <td>A Touching Saga of a Madman And a Forensic Psy...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>6</td>
      <td>0.99</td>
      <td>111</td>
      <td>12.99</td>
      <td>R</td>
      <td>Commentaries,Deleted Scenes</td>
      <td>2011-09-14 18:05:55</td>
    </tr>
    <tr>
      <th>377</th>
      <td>977</td>
      <td>WINDOW SIDE</td>
      <td>A Astounding Character Study of a Womanizer An...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>3</td>
      <td>2.99</td>
      <td>85</td>
      <td>25.99</td>
      <td>R</td>
      <td>Deleted Scenes,Behind the Scenes</td>
      <td>2011-09-14 18:05:55</td>
    </tr>
    <tr>
      <th>378</th>
      <td>978</td>
      <td>WISDOM WORKER</td>
      <td>A Unbelieveable Saga of a Forensic Psychologis...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>3</td>
      <td>0.99</td>
      <td>98</td>
      <td>12.99</td>
      <td>R</td>
      <td>Deleted Scenes,Behind the Scenes</td>
      <td>2011-09-14 18:05:55</td>
    </tr>
    <tr>
      <th>379</th>
      <td>980</td>
      <td>WIZARD COLDBLOODED</td>
      <td>A Lacklusture Display of a Robot And a Girl wh...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>4</td>
      <td>4.99</td>
      <td>75</td>
      <td>12.99</td>
      <td>PG</td>
      <td>Commentaries,Deleted Scenes,Behind the Scenes</td>
      <td>2011-09-14 18:05:55</td>
    </tr>
    <tr>
      <th>380</th>
      <td>982</td>
      <td>WOMEN DORADO</td>
      <td>A Insightful Documentary of a Waitress And a B...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>4</td>
      <td>0.99</td>
      <td>126</td>
      <td>23.99</td>
      <td>R</td>
      <td>Deleted Scenes,Behind the Scenes</td>
      <td>2011-09-14 18:05:56</td>
    </tr>
    <tr>
      <th>381</th>
      <td>983</td>
      <td>WON DARES</td>
      <td>A Unbelieveable Documentary of a Teacher And a...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>7</td>
      <td>2.99</td>
      <td>105</td>
      <td>18.99</td>
      <td>PG</td>
      <td>Behind the Scenes</td>
      <td>2011-09-14 18:05:56</td>
    </tr>
    <tr>
      <th>382</th>
      <td>985</td>
      <td>WONDERLAND CHRISTMAS</td>
      <td>A Awe-Inspiring Character Study of a Waitress ...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>4</td>
      <td>4.99</td>
      <td>111</td>
      <td>19.99</td>
      <td>PG</td>
      <td>Commentaries</td>
      <td>2011-09-14 18:05:56</td>
    </tr>
    <tr>
      <th>383</th>
      <td>987</td>
      <td>WORDS HUNTER</td>
      <td>A Action-Packed Reflection of a Composer And a...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>3</td>
      <td>2.99</td>
      <td>116</td>
      <td>13.99</td>
      <td>PG</td>
      <td>Trailers,Commentaries,Deleted Scenes</td>
      <td>2011-09-14 18:05:56</td>
    </tr>
    <tr>
      <th>384</th>
      <td>988</td>
      <td>WORKER TARZAN</td>
      <td>A Action-Packed Yarn of a Secret Agent And a T...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>7</td>
      <td>2.99</td>
      <td>139</td>
      <td>26.99</td>
      <td>R</td>
      <td>Trailers,Commentaries,Behind the Scenes</td>
      <td>2011-09-14 18:05:56</td>
    </tr>
    <tr>
      <th>385</th>
      <td>989</td>
      <td>WORKING MICROCOSMOS</td>
      <td>A Stunning Epistle of a Dentist And a Dog who ...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>4</td>
      <td>4.99</td>
      <td>74</td>
      <td>22.99</td>
      <td>R</td>
      <td>Commentaries,Deleted Scenes</td>
      <td>2011-09-14 18:05:56</td>
    </tr>
    <tr>
      <th>386</th>
      <td>991</td>
      <td>WORST BANGER</td>
      <td>A Thrilling Drama of a Madman And a Dentist wh...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>4</td>
      <td>2.99</td>
      <td>185</td>
      <td>26.99</td>
      <td>PG</td>
      <td>Deleted Scenes,Behind the Scenes</td>
      <td>2011-09-14 18:05:56</td>
    </tr>
    <tr>
      <th>387</th>
      <td>995</td>
      <td>YENTL IDAHO</td>
      <td>A Amazing Display of a Robot And a Astronaut w...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>5</td>
      <td>4.99</td>
      <td>86</td>
      <td>11.99</td>
      <td>R</td>
      <td>Trailers,Commentaries,Deleted Scenes</td>
      <td>2011-09-14 18:05:56</td>
    </tr>
    <tr>
      <th>388</th>
      <td>999</td>
      <td>ZOOLANDER FICTION</td>
      <td>A Fateful Reflection of a Waitress And a Boat ...</td>
      <td>2006</td>
      <td>1</td>
      <td>None</td>
      <td>5</td>
      <td>2.99</td>
      <td>101</td>
      <td>28.99</td>
      <td>R</td>
      <td>Trailers,Deleted Scenes</td>
      <td>2011-09-14 18:05:56</td>
    </tr>
  </tbody>
</table>
<p>389 rows × 13 columns</p>
</div>



### Aggregate Functions


```python
query = '''SELECT rating, AVG(rental_rate)
            FROM film
            GROUP BY rating;'''
pd.read_sql(query,con)
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>rating</th>
      <th>AVG(rental_rate)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>G</td>
      <td>2.888876</td>
    </tr>
    <tr>
      <th>1</th>
      <td>NC-17</td>
      <td>2.970952</td>
    </tr>
    <tr>
      <th>2</th>
      <td>PG</td>
      <td>3.051856</td>
    </tr>
    <tr>
      <th>3</th>
      <td>PG-13</td>
      <td>3.034843</td>
    </tr>
    <tr>
      <th>4</th>
      <td>R</td>
      <td>2.938718</td>
    </tr>
  </tbody>
</table>
</div>




```python
query = '''SELECT COUNT(customer_id)
            FROM customer;
        '''
pd.read_sql(query,con)
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>COUNT(customer_id)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>599</td>
    </tr>
  </tbody>
</table>
</div>




```python
query = '''SELECT MAX(customer_id), MIN(customer_id), AVG(customer_id), SUM(customer_id)
            FROM customer;
        '''
pd.read_sql(query,con)
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>MAX(customer_id)</th>
      <th>MIN(customer_id)</th>
      <th>AVG(customer_id)</th>
      <th>SUM(customer_id)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>599</td>
      <td>1</td>
      <td>300.0</td>
      <td>179700</td>
    </tr>
  </tbody>
</table>
</div>



### SQL Wildcards
Used to substitute for any other characters in a string. The wildcard characters are used with the LIKE operator. The LIKE operator is used in a WHERE clause to search for a specified pattern in a column


```python
#First the % wildcard is a substitute for zero or more characters
#Select any cusomers whose first name starts with M
query = '''SELECT *
            FROM customer
            WHERE first_name LIKE 'M%'; '''
pd.read_sql(query,con).head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>customer_id</th>
      <th>store_id</th>
      <th>first_name</th>
      <th>last_name</th>
      <th>email</th>
      <th>address_id</th>
      <th>active</th>
      <th>create_date</th>
      <th>last_update</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>MARY</td>
      <td>SMITH</td>
      <td>MARY.SMITH@sakilacustomer.org</td>
      <td>5</td>
      <td>1</td>
      <td>2006-02-14 22:04:36.000</td>
      <td>2011-09-14 18:10:28</td>
    </tr>
    <tr>
      <th>1</th>
      <td>7</td>
      <td>1</td>
      <td>MARIA</td>
      <td>MILLER</td>
      <td>MARIA.MILLER@sakilacustomer.org</td>
      <td>11</td>
      <td>1</td>
      <td>2006-02-14 22:04:36.000</td>
      <td>2011-09-14 18:10:28</td>
    </tr>
    <tr>
      <th>2</th>
      <td>9</td>
      <td>2</td>
      <td>MARGARET</td>
      <td>MOORE</td>
      <td>MARGARET.MOORE@sakilacustomer.org</td>
      <td>13</td>
      <td>1</td>
      <td>2006-02-14 22:04:36.000</td>
      <td>2011-09-14 18:10:28</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>1</td>
      <td>MICHELLE</td>
      <td>CLARK</td>
      <td>MICHELLE.CLARK@sakilacustomer.org</td>
      <td>25</td>
      <td>1</td>
      <td>2006-02-14 22:04:36.000</td>
      <td>2011-09-14 18:10:28</td>
    </tr>
    <tr>
      <th>4</th>
      <td>30</td>
      <td>1</td>
      <td>MELISSA</td>
      <td>KING</td>
      <td>MELISSA.KING@sakilacustomer.org</td>
      <td>34</td>
      <td>1</td>
      <td>2006-02-14 22:04:36.000</td>
      <td>2011-09-14 18:10:29</td>
    </tr>
  </tbody>
</table>
</div>




```python
#The _ wildcard is a substitute for a single character
#Select any customers whose last name ends with ING and has exactly 1 character before the ING
query = '''SELECT *
            FROM customer
            WHERE last_name LIKE '_ING';'''
pd.read_sql(query,con)
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>customer_id</th>
      <th>store_id</th>
      <th>first_name</th>
      <th>last_name</th>
      <th>email</th>
      <th>address_id</th>
      <th>active</th>
      <th>create_date</th>
      <th>last_update</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>30</td>
      <td>1</td>
      <td>MELISSA</td>
      <td>KING</td>
      <td>MELISSA.KING@sakilacustomer.org</td>
      <td>34</td>
      <td>1</td>
      <td>2006-02-14 22:04:36.000</td>
      <td>2011-09-14 18:10:29</td>
    </tr>
  </tbody>
</table>
</div>




```python
#The [character_list] wildcard sets ranges of characters to match
#Select any customers whose first name begins with a G or T, or F
query = '''SELECT *
            FROM customer
            WHERE first_name GLOB '[G,T,F]*';
        '''
pd.read_sql(query,con).head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>customer_id</th>
      <th>store_id</th>
      <th>first_name</th>
      <th>last_name</th>
      <th>email</th>
      <th>address_id</th>
      <th>active</th>
      <th>create_date</th>
      <th>last_update</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>47</td>
      <td>1</td>
      <td>FRANCES</td>
      <td>PARKER</td>
      <td>FRANCES.PARKER@sakilacustomer.org</td>
      <td>51</td>
      <td>1</td>
      <td>2006-02-14 22:04:36.000</td>
      <td>2011-09-14 18:10:29</td>
    </tr>
    <tr>
      <th>1</th>
      <td>54</td>
      <td>1</td>
      <td>TERESA</td>
      <td>ROGERS</td>
      <td>TERESA.ROGERS@sakilacustomer.org</td>
      <td>58</td>
      <td>1</td>
      <td>2006-02-14 22:04:36.000</td>
      <td>2011-09-14 18:10:29</td>
    </tr>
    <tr>
      <th>2</th>
      <td>56</td>
      <td>1</td>
      <td>GLORIA</td>
      <td>COOK</td>
      <td>GLORIA.COOK@sakilacustomer.org</td>
      <td>60</td>
      <td>1</td>
      <td>2006-02-14 22:04:36.000</td>
      <td>2011-09-14 18:10:29</td>
    </tr>
    <tr>
      <th>3</th>
      <td>72</td>
      <td>2</td>
      <td>THERESA</td>
      <td>WATSON</td>
      <td>THERESA.WATSON@sakilacustomer.org</td>
      <td>76</td>
      <td>1</td>
      <td>2006-02-14 22:04:36.000</td>
      <td>2011-09-14 18:10:30</td>
    </tr>
    <tr>
      <th>4</th>
      <td>75</td>
      <td>2</td>
      <td>TAMMY</td>
      <td>SANDERS</td>
      <td>TAMMY.SANDERS@sakilacustomer.org</td>
      <td>79</td>
      <td>1</td>
      <td>2006-02-14 22:04:36.000</td>
      <td>2011-09-14 18:10:30</td>
    </tr>
  </tbody>
</table>
</div>



### ORDER BY Keyword
Used to sort the result by one or more columns. Default sort order is ascending. To sort in descending order, use the DESC keyword. The syntax is:
SELECT column_name 
FROM table_name
ORDER BY column_name ASC|DESC

```python
query = '''SELECT * FROM customer
            ORDER BY last_name
        '''
pd.read_sql(query,con).head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>customer_id</th>
      <th>store_id</th>
      <th>first_name</th>
      <th>last_name</th>
      <th>email</th>
      <th>address_id</th>
      <th>active</th>
      <th>create_date</th>
      <th>last_update</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>505</td>
      <td>1</td>
      <td>RAFAEL</td>
      <td>ABNEY</td>
      <td>RAFAEL.ABNEY@sakilacustomer.org</td>
      <td>510</td>
      <td>1</td>
      <td>2006-02-14 22:04:37.000</td>
      <td>2011-09-14 18:10:42</td>
    </tr>
    <tr>
      <th>1</th>
      <td>504</td>
      <td>1</td>
      <td>NATHANIEL</td>
      <td>ADAM</td>
      <td>NATHANIEL.ADAM@sakilacustomer.org</td>
      <td>509</td>
      <td>1</td>
      <td>2006-02-14 22:04:37.000</td>
      <td>2011-09-14 18:10:42</td>
    </tr>
    <tr>
      <th>2</th>
      <td>36</td>
      <td>2</td>
      <td>KATHLEEN</td>
      <td>ADAMS</td>
      <td>KATHLEEN.ADAMS@sakilacustomer.org</td>
      <td>40</td>
      <td>1</td>
      <td>2006-02-14 22:04:36.000</td>
      <td>2011-09-14 18:10:29</td>
    </tr>
    <tr>
      <th>3</th>
      <td>96</td>
      <td>1</td>
      <td>DIANA</td>
      <td>ALEXANDER</td>
      <td>DIANA.ALEXANDER@sakilacustomer.org</td>
      <td>100</td>
      <td>1</td>
      <td>2006-02-14 22:04:36.000</td>
      <td>2011-09-14 18:10:30</td>
    </tr>
    <tr>
      <th>4</th>
      <td>470</td>
      <td>1</td>
      <td>GORDON</td>
      <td>ALLARD</td>
      <td>GORDON.ALLARD@sakilacustomer.org</td>
      <td>475</td>
      <td>1</td>
      <td>2006-02-14 22:04:37.000</td>
      <td>2011-09-14 18:10:41</td>
    </tr>
  </tbody>
</table>
</div>




```python
query = '''SELECT * FROM customer
            ORDER BY last_name DESC;'''
pd.read_sql(query,con).head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>customer_id</th>
      <th>store_id</th>
      <th>first_name</th>
      <th>last_name</th>
      <th>email</th>
      <th>address_id</th>
      <th>active</th>
      <th>create_date</th>
      <th>last_update</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>28</td>
      <td>1</td>
      <td>CYNTHIA</td>
      <td>YOUNG</td>
      <td>CYNTHIA.YOUNG@sakilacustomer.org</td>
      <td>32</td>
      <td>1</td>
      <td>2006-02-14 22:04:36.000</td>
      <td>2011-09-14 18:10:29</td>
    </tr>
    <tr>
      <th>1</th>
      <td>413</td>
      <td>2</td>
      <td>MARVIN</td>
      <td>YEE</td>
      <td>MARVIN.YEE@sakilacustomer.org</td>
      <td>418</td>
      <td>1</td>
      <td>2006-02-14 22:04:37.000</td>
      <td>2011-09-14 18:10:40</td>
    </tr>
    <tr>
      <th>2</th>
      <td>402</td>
      <td>1</td>
      <td>LUIS</td>
      <td>YANEZ</td>
      <td>LUIS.YANEZ@sakilacustomer.org</td>
      <td>407</td>
      <td>1</td>
      <td>2006-02-14 22:04:37.000</td>
      <td>2011-09-14 18:10:39</td>
    </tr>
    <tr>
      <th>3</th>
      <td>318</td>
      <td>1</td>
      <td>BRIAN</td>
      <td>WYMAN</td>
      <td>BRIAN.WYMAN@sakilacustomer.org</td>
      <td>323</td>
      <td>1</td>
      <td>2006-02-14 22:04:37.000</td>
      <td>2011-09-14 18:10:37</td>
    </tr>
    <tr>
      <th>4</th>
      <td>31</td>
      <td>2</td>
      <td>BRENDA</td>
      <td>WRIGHT</td>
      <td>BRENDA.WRIGHT@sakilacustomer.org</td>
      <td>35</td>
      <td>1</td>
      <td>2006-02-14 22:04:36.000</td>
      <td>2011-09-14 18:10:29</td>
    </tr>
  </tbody>
</table>
</div>



### GROUP BY
Used with the aggregate functions to group the results by one or more columns. The syntax is:
SELECT column_name, aggregate_function(column_name) 
FROM table_name 
WHERE column_name operator value 
GROUP BY column_name;

```python
#Count the number of customers per store and group them by store ID
query = '''SELECT store_id, COUNT(customer_id)
            FROM customer
            GROUP BY store_id;
        '''
pd.read_sql(query,con)
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>store_id</th>
      <th>COUNT(customer_id)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>326</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>273</td>
    </tr>
  </tbody>
</table>
</div>




```python
query = '''SELECT active, MAX(customer_id) 
            FROM customer
            GROUP BY active; '''
pd.read_sql(query,con)
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>active</th>
      <th>MAX(customer_id)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>592</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>599</td>
    </tr>
  </tbody>
</table>
</div>




```python
query = '''CREATE TABLE celebs(
            id INTEGER,
            name TEXT,
            age INTEGER
            );'''
pd.read_sql(query,con)
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-23-dc5f56bb8bd8> in <module>()
          4             age INTEGER
          5             );'''
    ----> 6 pd.read_sql(query,con)
    

    C:\Users\masof\Anaconda3\lib\site-packages\pandas\io\sql.py in read_sql(sql, con, index_col, coerce_float, params, parse_dates, columns, chunksize)
        497             sql, index_col=index_col, params=params,
        498             coerce_float=coerce_float, parse_dates=parse_dates,
    --> 499             chunksize=chunksize)
        500 
        501     try:
    

    C:\Users\masof\Anaconda3\lib\site-packages\pandas\io\sql.py in read_query(self, sql, index_col, coerce_float, params, parse_dates, chunksize)
       1594         args = _convert_params(sql, params)
       1595         cursor = self.execute(*args)
    -> 1596         columns = [col_desc[0] for col_desc in cursor.description]
       1597 
       1598         if chunksize is not None:
    

    TypeError: 'NoneType' object is not iterable



```python

```
