# Trip Tracking Star Schema
#### At a very high level, I would consider the following in the design of a dimensional star schema for tracking the trip details.
### 1. Identify the business process we want to track
In the given scenario, the business is interested in tracking the following measures:

•	Daily trips taken

•	Duration of trips

•	Miles driven

### 2. Choose the granularity of the fact data
This will depend on the total volume of transaction-level data. It’s usually a good idea to start with the finest grain of data and store each Trip transaction line item.

### 3. Strip out the dimensions
Identify the attributes involved in each transaction and create separate dimension tables for them. Each record in the dimension table should be unique and have a numeric primary key associated to it. Here Driver, Profile, Vehicle and Calendar (dates) are all dimensions of the Trip tracking.

![dimensions](https://user-images.githubusercontent.com/47398796/52384856-33b72600-2a4d-11e9-9dc0-0be8a4bbae44.png)

### 4. Consolidate the facts
The remaining metrics like Trip Count, Trip Distance and Trip Duration are the measures and belong in a fact table. Alongside each measure, we should have foreign keys that reference all dimensions involved in the process like Driver, Profile, Vehicle and Calendar.

#### So, at the very high level, the following represents the Star schema for this scenario:

![trip_tracking_star_schema](https://user-images.githubusercontent.com/47398796/52368464-73194e80-2a1c-11e9-83df-dc7149938a78.png)

### Note:
This data mart can answer questions like:

1. How many trips taken Daily (Trip Count (Set equal to 1) so can be by users)?
2. What is the duration of the Trip taken (calculated as Started_at – Ended_at)?
3. How many miles driven in the given trip?

Here, Driver_ID, Vechile_ID and Profile_ID are the Degenerative keys for the respective tables Dim_Driver, Dim_Vehicle and Dim_Profile. To make this design more robust, things like Averages, Counts, Totals, KPI’s, Graphs, Trends and other derived figures can be considered to the facts as well.
