# Analyse_eBay_Sales_Cars

# This Project 
The aim of this project is to explore dataset of used carsfrom eBay Kleinanzeigen, a classifieds section of the German eBay website. I use this project to highlight my skills in 
1. Deal with incorrect data
2. Analyze the price difference and the correlation between its and mileage.


# My Analysis
You can find [my full analysis](https://github.com/NguyenDangXuanLinh/eBay_Car_Sales_Data/blob/main/Exploring%20eBay%20Car%20Sales.ipynb) in this notebook 
<br>

## 1. Deal with incorrect Registeration Data
```
autos["registration_year"].describe() 
```
<img aligh=center width="314" alt="car1" src="https://github.com/NguyenDangXuanLinh/eBay_Car_Sales_Data/assets/140143092/387d9cca-757a-4b84-84a5-37574348bd91">


 According to the information in registration_year column, the oldest car were registered in 1000 which is not supposed to be true, because it is far before first car was invented, while maximum year 9999, that does not seem realistic too, as it is in future. So we have to correct the data in registration_year column.
<br>

## 2. Correlation between price and mileage
```
brand_mean_mileage= {}
for brand in top_10_brands.index:
    brand_only = autos[autos['brand'] == brand]
    mean_mileage = brand_only['km'].mean()
    brand_mean_mileage[brand]= int(mean_mileage)
    
mean_mileage = pd.Series(brand_mean_mileage).sort_values(ascending=False)
mean_price = pd.Series(brand_mean_price).sort_values(ascending=False)
brand_info= pd.DataFrame(mean_mileage, columns=['mean_mileage'])
brand_info['mean_price'] = mean_price
brand_info
```
<img align=center width="337" alt="car2" src="https://github.com/NguyenDangXuanLinh/eBay_Car_Sales_Data/assets/140143092/bb3b18ed-5b73-4e37-a42e-92e607061df5">

> The range of car mileages does not vary as much as the prices do by brand, instead all falling within 10% for the top brands. There is a slight trend to the more expensive vehicles having higher mileage, with the less expensive vehicles having lower mileage.

```
brand_reg_year = {}

for brand in top_10_brands.index:
    brand_in = autos[autos['brand'] == brand]
    mean_year = brand_in['registration_year'].mean()
    brand_reg_year[brand] = int(mean_year)
brand_reg_year
```

{'volkswagen': 2002,\
 'bmw': 2002,\
 'opel': 2002,\
 'mercedes_benz': 2001,\
 'audi': 2003,\
 'ford': 2002,\
 'renault': 2002,\
 'peugeot': 2003,\
 'fiat': 2002,\
 'seat': 2004}
 > Most cars from the top 10 brands were registered between year 2002 - 2004. This shows that majority of the cars listed are at least 12 years old.
<br>

# My findings
```
top_10_dist = {}

for b in top_10_brands.index:
    dist = top_10_brands[b]
    price_dist = round((dist * 100),1)
    top_10_dist[b] = price_dist

brand_dist = pd.Series(top_10_dist).sort_values(ascending=False)
brand_info['distribution(%)'] = brand_dist
brand_year = pd.Series(brand_reg_year).sort_values(ascending=False)
brand_info['registration_mean_year'] = brand_year
brand_info
```

<img align=center width="624" alt="car3" src="https://github.com/NguyenDangXuanLinh/eBay_Car_Sales_Data/assets/140143092/e21386fe-da6a-49f1-a559-f1e88bba4dfd">

Car listings on eBay Gemrany are dominated by the German brands.

- Volkswagen is by far the most common brand with over 20 % dominance.
- Most vehicles have a milages well over 125,000 km.
- The prices are evenly distributed from 8700 to 14000.
Top 3 brands in price are over $15,000 per car. Majority of the vehicles were registered early 2000s.






