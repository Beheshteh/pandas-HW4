
 


Analyzing Data for fantasy game Heroes of Pymoli. 

This is a free-to-play, but players are encouraged to purchase optional items that enhance their playing experience. Below are three important observation I have from these data.

•	Men play more (82% of the players of this game are Males) and they also create more revenue. Please check DataFrame on Gender demographics and total purchase based on the gender.
•	The age group of 20-24 spent most and created more revenue than any other age group. Please check DataFrame on Age demographics.
•	Most popular items and most profitable items are very different as far as their prices. In both data set there is one item in common between these two categories which is not the cheapest one. In general, you create more profit with more expensive item. Please check DataFrame on 5 most popular and profitable items.


```python
import json
import pandas as pd
```


```python
#filename = input("what is the name of .json file you would like to analize?")
```


```python
indata_pd = pd.read_json('purchase_data2.json')
indata_pd.head(5)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>20</td>
      <td>Male</td>
      <td>93</td>
      <td>Apocalyptic Battlescythe</td>
      <td>4.49</td>
      <td>Iloni35</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>12</td>
      <td>Dawne</td>
      <td>3.36</td>
      <td>Aidaira26</td>
    </tr>
    <tr>
      <th>2</th>
      <td>17</td>
      <td>Male</td>
      <td>5</td>
      <td>Putrid Fan</td>
      <td>2.63</td>
      <td>Irim47</td>
    </tr>
    <tr>
      <th>3</th>
      <td>17</td>
      <td>Male</td>
      <td>123</td>
      <td>Twilight's Carver</td>
      <td>2.55</td>
      <td>Irith83</td>
    </tr>
    <tr>
      <th>4</th>
      <td>22</td>
      <td>Male</td>
      <td>154</td>
      <td>Feral Katana</td>
      <td>4.11</td>
      <td>Philodil43</td>
    </tr>
  </tbody>
</table>
</div>




```python
#      Player Count

# Total Number of Players
player_unique = indata_pd.groupby("SN")
totalUniquePlayer = len(player_unique)
totalUniquePlayer
```




    74




```python
#Purchasing Analysis (Total) 

# Number of unique items
# Average Purchase Price
# Number of Purchase 
# Total Revenue
item_group = indata_pd.groupby("Item ID")
new_table = pd.DataFrame({
                         "Number of unique items": len(item_group),
                         "Average Price": item_group["Price"].mean(),
                         "Number of Purchase":(item_group["Item ID"].value_counts()).sum(),
                         "Total Revenue": item_group["Price"].mean() * 
                                          (item_group["Item ID"].value_counts()).sum()
})
new_table.index.name ="Purchasing Analysis (Total)"

new_table.head(5)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Price</th>
      <th>Number of Purchase</th>
      <th>Number of unique items</th>
      <th>Total Revenue</th>
    </tr>
    <tr>
      <th>Purchasing Analysis (Total)</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.89</td>
      <td>78</td>
      <td>64</td>
      <td>147.42</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3.67</td>
      <td>78</td>
      <td>64</td>
      <td>286.26</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2.65</td>
      <td>78</td>
      <td>64</td>
      <td>206.70</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1.91</td>
      <td>78</td>
      <td>64</td>
      <td>148.98</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2.63</td>
      <td>78</td>
      <td>64</td>
      <td>205.14</td>
    </tr>
  </tbody>
</table>
</div>




```python
#      Gender Demographics
# Count of Male, Female and Non_Disclosed Players
# Percentage of Male, Female and Non_Disclosed Players

Player_group = indata_pd.groupby("Gender")
totalNumPlayer = len(indata_pd)

new_table = pd.DataFrame({
                         "Count of Gender": Player_group["Gender"].size(),
                         "Percentage of Gender": round((Player_group["Gender"].size() / 
                                                       totalNumPlayer * 100),2),
                         })

new_table.index.name ="Gender Demographics"

new_table
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Count of Gender</th>
      <th>Percentage of Gender</th>
    </tr>
    <tr>
      <th>Gender Demographics</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>13</td>
      <td>16.67</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>64</td>
      <td>82.05</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>1</td>
      <td>1.28</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Purchasing Analysis (Gender) 

# The below each broken by gender
# Purchase Count
# Average Purchase Price
# Total Purchase Value
# Normalized Totals

new_table = pd.DataFrame({
                         "Average Price": Player_group["Price"].mean(),
                         "Purchases count": Player_group["Item ID"].size(),
                         "Total Revenue": Player_group["Price"].sum(),
                         "Normalized total": round(Player_group["Price"].sum() / 
                                                   Player_group["Gender"].size(),3)
})
new_table.index.name ="Purchasing Analysis (Gender)"

new_table
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Price</th>
      <th>Normalized total</th>
      <th>Purchases count</th>
      <th>Total Revenue</th>
    </tr>
    <tr>
      <th>Purchasing Analysis (Gender)</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>3.183077</td>
      <td>3.183</td>
      <td>13</td>
      <td>41.38</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>2.884375</td>
      <td>2.884</td>
      <td>64</td>
      <td>184.60</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>2.120000</td>
      <td>2.120</td>
      <td>1</td>
      <td>2.12</td>
    </tr>
  </tbody>
</table>
</div>




```python
#      Age Demographics

# The below each broken into bins of 4 years (i.e. &lt;10, 10-14, 15-19, etc.) 
#AgeGroup
age_bins=[0, 10, 14, 19, 24, 29, 34, 39, 44, 49]
agegroupName = ["<10", "10-14", "15-19", "20-24", "25-29", "30-34", "35-39", "40-44", "45-49"]
indata_pd["AgeLable"] = pd.cut(indata_pd["Age"], age_bins, labels = agegroupName)
#indata_pd_indexed_on_age = indata_pd.set_index('AgeLable')
indata_pd.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
      <th>AgeLable</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>20</td>
      <td>Male</td>
      <td>93</td>
      <td>Apocalyptic Battlescythe</td>
      <td>4.49</td>
      <td>Iloni35</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>12</td>
      <td>Dawne</td>
      <td>3.36</td>
      <td>Aidaira26</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>2</th>
      <td>17</td>
      <td>Male</td>
      <td>5</td>
      <td>Putrid Fan</td>
      <td>2.63</td>
      <td>Irim47</td>
      <td>15-19</td>
    </tr>
    <tr>
      <th>3</th>
      <td>17</td>
      <td>Male</td>
      <td>123</td>
      <td>Twilight's Carver</td>
      <td>2.55</td>
      <td>Irith83</td>
      <td>15-19</td>
    </tr>
    <tr>
      <th>4</th>
      <td>22</td>
      <td>Male</td>
      <td>154</td>
      <td>Feral Katana</td>
      <td>4.11</td>
      <td>Philodil43</td>
      <td>20-24</td>
    </tr>
  </tbody>
</table>
</div>




```python

Age_group = indata_pd.groupby("AgeLable")
NumPlayerperAge = indata_pd.groupby("AgeLable").size()
 
#Purchase Count
#Average Purchase Price
#Total Purchase Value
#Normalized Totals
new_table = pd.DataFrame({
                         "Purchase Count": Age_group["Item Name"].size(),
                         "Average Purchase Price": round(Age_group["Price"].mean(), 2),
                         "Total Purchase Value": Age_group["Price"].sum(),
                         "Normalized total": round(Age_group["Price"].sum() / 
                                                   NumPlayerperAge, 2)
})
new_table.index.name ="Age Demographics"

new_table
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Purchase Price</th>
      <th>Normalized total</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Age Demographics</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>2.76</td>
      <td>2.76</td>
      <td>5</td>
      <td>13.82</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>2.99</td>
      <td>2.99</td>
      <td>3</td>
      <td>8.96</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>2.76</td>
      <td>2.76</td>
      <td>11</td>
      <td>30.41</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>3.02</td>
      <td>3.02</td>
      <td>36</td>
      <td>108.89</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>2.90</td>
      <td>2.90</td>
      <td>9</td>
      <td>26.11</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>1.98</td>
      <td>1.98</td>
      <td>7</td>
      <td>13.89</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>3.56</td>
      <td>3.56</td>
      <td>6</td>
      <td>21.37</td>
    </tr>
    <tr>
      <th>40-44</th>
      <td>4.65</td>
      <td>4.65</td>
      <td>1</td>
      <td>4.65</td>
    </tr>
    <tr>
      <th>45-49</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
#          Top Spenders

# Identify the top 5 spenders in the game by total purchase value, then list (in a table):
# SN
# Purchase Count
# Average Purchase Price
# Total Purchase Value

# Identify the top 5 spenders in the game by total purchase value
listofspender = player_unique["Price"].sum().nlargest(5)
listofspender_df = pd.DataFrame(listofspender)
listofspender_df['Purchase count'] = player_unique['Item ID'].size()
listofspender_df['Average Purchase price'] = player_unique['Price'].mean()
listofspender_df['Total Purchase price'] = player_unique['Price'].sum()
listofspender_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Price</th>
      <th>Purchase count</th>
      <th>Average Purchase price</th>
      <th>Total Purchase price</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Sundaky74</th>
      <td>7.41</td>
      <td>2</td>
      <td>3.705</td>
      <td>7.41</td>
    </tr>
    <tr>
      <th>Aidaira26</th>
      <td>5.13</td>
      <td>2</td>
      <td>2.565</td>
      <td>5.13</td>
    </tr>
    <tr>
      <th>Eusty71</th>
      <td>4.81</td>
      <td>1</td>
      <td>4.810</td>
      <td>4.81</td>
    </tr>
    <tr>
      <th>Chanirra64</th>
      <td>4.78</td>
      <td>1</td>
      <td>4.780</td>
      <td>4.78</td>
    </tr>
    <tr>
      <th>Alarap40</th>
      <td>4.71</td>
      <td>1</td>
      <td>4.710</td>
      <td>4.71</td>
    </tr>
  </tbody>
</table>
</div>




```python
#         Most Popular Items

# Identify the 5 most popular items by purchase count, then list (in a table):
# Item ID
# Item Name
# Purchase Count
# Item Price
# Total Purchase Value

# Identify the top 5 spenders in the game by total purchase value
item_price_group = indata_pd.groupby(["Item ID", "Item Name", "Price"])
listofPItem = item_price_group["Item Name"].size().nlargest(5)
listofPItem_df = pd.DataFrame(listofPItem)
listofPItem_df['Purchase Count'] = item_price_group["Item Name"].size()
listofPItem_df['Total Purchase Value'] = item_price_group["Price"].sum()

listofPItem_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th></th>
      <th>Item Name</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>94</th>
      <th>Mourning Blade</th>
      <th>3.64</th>
      <td>3</td>
      <td>3</td>
      <td>10.92</td>
    </tr>
    <tr>
      <th>60</th>
      <th>Wolf</th>
      <th>2.70</th>
      <td>2</td>
      <td>2</td>
      <td>5.40</td>
    </tr>
    <tr>
      <th>64</th>
      <th>Fusion Pummel</th>
      <th>2.42</th>
      <td>2</td>
      <td>2</td>
      <td>4.84</td>
    </tr>
    <tr>
      <th>90</th>
      <th>Betrayer</th>
      <th>4.12</th>
      <td>2</td>
      <td>2</td>
      <td>8.24</td>
    </tr>
    <tr>
      <th>93</th>
      <th>Apocalyptic Battlescythe</th>
      <th>4.49</th>
      <td>2</td>
      <td>2</td>
      <td>8.98</td>
    </tr>
  </tbody>
</table>
</div>




```python
#        Most Profitable Items

# Identify the 5 most profitable items by total purchase value, then list (in a table):
# Item ID
# Item Name
# Purchase Count
# Item Price
# Total Purchase Value

listofProfitableItem = item_price_group["Price"].sum().nlargest(5)
listofProfitableItem_df = pd.DataFrame(listofProfitableItem)
listofProfitableItem_df['Purchase Count'] = item_price_group["Item Name"].size()
listofProfitableItem_df['Total Purchase Value'] = item_price_group["Price"].sum()

listofProfitableItem_df

```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th></th>
      <th>Price</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>94</th>
      <th>Mourning Blade</th>
      <th>3.64</th>
      <td>10.92</td>
      <td>3</td>
      <td>10.92</td>
    </tr>
    <tr>
      <th>117</th>
      <th>Heartstriker, Legacy of the Light</th>
      <th>4.71</th>
      <td>9.42</td>
      <td>2</td>
      <td>9.42</td>
    </tr>
    <tr>
      <th>93</th>
      <th>Apocalyptic Battlescythe</th>
      <th>4.49</th>
      <td>8.98</td>
      <td>2</td>
      <td>8.98</td>
    </tr>
    <tr>
      <th>90</th>
      <th>Betrayer</th>
      <th>4.12</th>
      <td>8.24</td>
      <td>2</td>
      <td>8.24</td>
    </tr>
    <tr>
      <th>154</th>
      <th>Feral Katana</th>
      <th>4.11</th>
      <td>8.22</td>
      <td>2</td>
      <td>8.22</td>
    </tr>
  </tbody>
</table>
</div>


