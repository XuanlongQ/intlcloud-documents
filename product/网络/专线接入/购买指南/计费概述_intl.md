## Billing of Connection
For Tencent Cloud Connection, a one-off charge of 2,500 USD is charged for each line. And Monthly Rental Charge is under planning, which you won't be charged until published.

## Billing of Dedicated Tunnel
The charge for Dedicated Tunnels depends on whether the Connection access point and the VPC are located in the same city:

- If they are in the same region, Dedicated Tunnel is free of charge.
- If they are in different regions and both endpoints are within Mainland China (excluding Hong Kong, Macao and Taiwan), a fee for domestic and cross-region interconnection is charged.
- If they are in different regions and at least one endpoint is located outside Mainland China (including Hong Kong, Macao and Taiwan), then consult with your business manager.

Special offer: Dedicated Tunnels between Beijing and Tianjin/Guangzhou and Shenzhen are free of charge until March 1, 2019. A further notice will be given before the end of the special offer.

**Billing method:** The fee for cross-region interconnection is charged by actual monthly bandwidth usage of a Dedicated Tunnel on a postpaid basis according to Monthly 95th Percentile (based on the average bandwidth per 5 minutes in a calendar month).

**Calculation method:**
Monthly fee for a Dedicated Tunnel = Peak bandwidth of Monthly 95th Percentile x Proportion of effective days x Tiered unit price 

Definitions:
**Peak bandwidth of Monthly 95th Percentile:** It is calculated on the basis of a calendar month. In a calendar month, sort the averages of bandwidth in every 5 minutes for all effective days (generating consumption) in ascending order and eliminate the highest 5% statistical points. Then take the largest bandwidth among the remaining 95% of statistical points as the peak bandwidth of Monthly 95th Percentile.
**Proportion of effective days:** An effective day refers to a day with at least one bandwidth value captured every 5 minutes greater than 3 Kbps. Proportion of effective days = Number of effective days of this month / Number of calendar days of this month.
**Tiered unit price**: The unit price of the corresponding tier. For example, if the peak bandwidth of Monthly 95th Percentile is 95 Mbps, the fee for this month = 95 x Tiered unit price [50-100 Mbps].

**Example:**
A client uses a Dedicated Tunnel for 14 effective days in January. The number of the statistic points for each day is 288 (24x60/5). The total number of the statistic points for 14 days is 4,032 (14x288). Sort the bandwidth values of all 4,032 statistic points in ascending order and eliminate the last 5%. Then take the (4032*0.95=3830.4) 3830th bandwidth as the billing bandwidth and mark it as Max95. The fee for January is: Max95 x 14/31 x Tiered unit price.

The tiered unit prices corresponding to the bandwidth usage are shown as below:

| Bandwidth (Mbps) | Mainland China (USD/Mbps)(MRC)|
| ------------------ | ------------ |
| [0 , 10)     | 85          |
| [10 , 20)     |  63        |
| [20 , 50)   | 45           | 
| [50 , 100)  | 34            | 
| [100 , 200)  | 25           |
| [200 , 500) | 18            |
| [500 , 1000) | 14           | 
| [1000 , 2000) | 11            | 
| [2000 , 1000000)        | 10            | 

*For the data interoperability between Mainland China and other regions, consult with your business manager.*

