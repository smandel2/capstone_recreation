# capstone_recreation
![alt text](https://raw.github.com/smandel2/capstone_recreation/master/images/tent_in_desert.jpg)

# Data Acquisition / Preprocessing

I obtained 2015 reservation data from the recreation.gov website, which consists of over 30 agencies including the National Park Service, the US Army Corps of Engineers, the Bureau of Land Management, USDA Forest Service and many other Federal agencies. From the data dictionary, I learned that there is a Camping dataset that links to the Reservations dataset. I mapped the camping data to the reservation data to only include camping related reservations using a lambda function.

Convert dates to be in datetime format so that they can be used in calculations. Ultimately we will be looking at the median Order Month and median Start Month for each park and using these as features in the model.

While I chose the 2015 Reservation dataset, there were cases that crossed over the year. To handle this, I set the OrderYear and StartYear to be 2015. Then I calculated the median order month and median start month for the parks and renamed the columns to reflect this.

Because the data is transactional -- reservations that were booked to campsites, it was necessary to group the data. For example, a single reservation at a park will contain all the pertinent data such as the order date, the total, whether it will be for tent camping or an RV, etc. I grouped all the reservations by park, and did a sum of all the relevant data.

# Create Regions and Map States to Regions

![alt text](https://raw.github.com/smandel2/capstone_recreation/master/images/region_map.jpg)

In looking at the data, there were some distinct differences across regions as far as things such as the type of the equipment used for camping, as well as the average start months. As a result, I created 10 regions and mapped each state to a region. The regions will be the target in my models.

Most of the null values resulted from categorical items such as Tent, RV, Van, Fifth Wheel, etc. Some items such as Boat had mostly null values and these columns were deleted. Most reservations consisted of one or two of these items. Note that these attributes are optional according to the data dictionary. I chose to impute the remaining null values to zero.

![alt text](https://raw.github.com/smandel2/capstone_recreation/master/images/maps.jpg)

The target variable is Region which had been created and mapped to State as mentioned above. Since region is mapped to State, I excluded State from the feature set.

# Modeling

Train, Test, Split – 67% for training set  and 33% for test set

The frequency of the most frequent class is 30.67%

Models used: Logistic Regression with GridSearchCV, Decision Tree Classifier, Random Forest Classifier, and Gradient Boost.

Gradient Boost yielded the best results – Accuracy Score 0.555

![alt text](https://raw.github.com/smandel2/capstone_recreation/master/images/feature_imp_gb.jpg)

![alt text](https://raw.github.com/smandel2/capstone_recreation/master/images/confusion_matrix_gb.png)


## Confusion Matrix Heat Map

![alt text](https://raw.github.com/smandel2/capstone_recreation/master/images/heat_map_cm.png)

![alt text](https://raw.github.com/smandel2/capstone_recreation/master/images/class_rep_gb.png)

# Next Steps

* Move sparse regions to an “Other” region
* Add weights to the model for Mountain and Pacific
* Rerun only the Mountain predictions in a new model
* Add data from 2014
