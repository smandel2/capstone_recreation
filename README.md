# capstone_recreation
![alt text](https://raw.github.com/smandel2/capstone_recreation/master/images/tent_in_desert.jpg)

# Data Aquisition / Preprocessing

I got the data from the recreation.gov website which consists of over 30 agencies including the National Park Service, the US Army Corps of Engineers, the Bureau of Land Management, USDA Forest Service and many other Federal agencies. In addition to downloading the data, I reviewed the data dictionary and looked at the Entity Relationship diagram. In my investigation, it turned out that there is a Camping dataset that links to the Reservations dataset. I mapped the data from the dataset and excluded the others as described later.

The camping specific dataset contains FacilityID which are specific to parks that have camping specific facilities. In order to only have camping-related reservationships, it was necessary to identify the unique FacilityIDs and then run a lambda function to map the Facility ID of the reservation dataset only to those in the Campsite dataset that match up with the unique FacilityID and assign it back to a new dataframe (df15Camp1a). It was also necessary to rename the FacilityID to match the same case as in the Campground dataset.

Convert dates to be in datetime format so that they can be used in calculations. Ultimately we will be looking at the median Order Month and median Start Month for each park and using these as features in the model.

While I chose the 2015 Reservation dataset, there were cases that crossed over the year. To handle this, I set the OrderYear and StartYear to be 2015. Then I calculated the mean order month and mean start month for the parks and renamed the columns to reflect this.

Because the data we are working with is transactional -- reservations that were booked to campsites, it was necessary to group the data. For example, a single reservation at a park will contain all the pertinent data such as the order date, the total, whether it will be for tent camping or an RV, etc. By grouping all the reservations per park, we can obtain the sums of all the relevant data.

# Create Regions and Map States to Regions

![alt text](https://raw.github.com/smandel2/capstone_recreation/master/images/region_map.jpg)
