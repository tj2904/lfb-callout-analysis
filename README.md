# London Fire Brigade (LFB) Callout Analysis

## Business Problems:
This dataset will be employed to answer the following questions:
* What are the trends of callouts? 
  *  By understanding trends resource allocation and be predicted and planned for.
* How frequently are incidents attended by services from outside the borough?
  * Knowing this will feed into the next question and illuminate how well covered the 
borough is, with the hypothesis being if it is well covered/resourced within the 
borough outside help won’t be required often.
* Are there incident location hotspots within the borough?
  * Along with the previous question knowing this can influence station location and 
when paired with response time information support the service to hit its 
response time targets.
* What factors predict a false alarm?
  * Being able to predict a false alarm could influence resource allocation decisions, 
every false alarm not attended represents a saving. Of course, false negatives 
carry potential heavy consequences.
* What factors are most associated with fires within dwellings?
  * Identifying the key risk factors for residential fires will support the LFB in its target 
to support the community and where fire prevention work would be best targeted.

## Data Pre-processing
### Data Types
To ensure that the correct datatypes were allocated to each variable `Easting_rounded`, 
`Northing_rounded` and `HourOfCall` needed converting to categorical types.

### Null/Missing Values
`SpecialServiceType` null values are not errors but refer to incidents not classed as a 
Special Service, `FirstPump_Arriving_AttendanceTime` has 513 null values. The vast 
majority of these refer to cases of Lift release, all are Special Service calls or False alarms, 
the `FirstPump_Arriving_DeployedFromStation` is also missing. Replacing the latter 
would not be helpful at all. It is inferred that a missing pump time indicates that the incident 
was attended by staff without a pump, so the missing values will be accepted, replacement 
would negatively impact the quality of the dataset, but they will be dropped/exclude if used 
for averaging etc. as to not drag the mean values down.

### Imbalanced classes
There is class imbalance within the variables that will be used for both decision tree and k-nearest neighbour (KNN) model construction. This will be addressed using the SMOTE 
algorithm to over-sample the minority classes.
Analysis also highlighted the imbalance in the data intended for use for Association Analysis, 
however, this is a categorical variable so will need to be encoded before use, this encoding 
will remove the need to scale or normalise the data.

### Model Construction
#### What are the trends of callouts? 
![image](https://github.com/tj2904/lfb-callout-analysis/assets/3164936/dd4ef23d-6b62-4e58-9a0e-732138a9a910)
![image](https://github.com/tj2904/lfb-callout-analysis/assets/3164936/0809e0b0-398a-4e30-87c3-4b2a9cc30379)

_More plots are in the [notebook](https://github.com/tj2904/lfb-callout-analysis/blob/main/LFB_Analysis.ipynb)_

It is clear that there is a rise in demand placed upon LFB, with more incidents being responded to, with a 
longer peak period than previously experienced. This has implications for future planning that should be considered. 

#### How frequently are incidents attended by services from outside the borough?
![image](https://github.com/tj2904/lfb-callout-analysis/assets/3164936/d9e5345f-bcb3-4052-9904-79b644108fd1)
![image](https://github.com/tj2904/lfb-callout-analysis/assets/3164936/571d364e-be60-45da-b618-e215dc7f1048)

![image](https://github.com/tj2904/lfb-callout-analysis/assets/3164936/5f7d315d-96e2-4daf-83ea-2826e230df83)

_More plots are in the [notebook](https://github.com/tj2904/lfb-callout-analysis/blob/main/LFB_Analysis.ipynb)_

For Hounslow there are a significant proportion of incidents that are supported by response from stations that are not 
inside the borough. This would benefit from further investigation by LFB, especially to determine if this pattern is 
unusual compared to the rest of London, and what impact it is having upon the cost of rendering this service.

#### Are there incident location hotspots within the borough?
![image](https://github.com/tj2904/lfb-callout-analysis/assets/3164936/33232d2e-dbb1-4d89-a806-0d79f57ecafb)
![image](https://github.com/tj2904/lfb-callout-analysis/assets/3164936/55555df5-5dca-41a6-92ca-527ec1347abe)
![image](https://github.com/tj2904/lfb-callout-analysis/assets/3164936/e15ee9fd-27ef-4f29-a6a3-f9577e6a8e13)

_More plots are in the [notebook](https://github.com/tj2904/lfb-callout-analysis/blob/main/LFB_Analysis.ipynb)_

Key locations within the borough have been identified, and it has been found that stations are located close to these 
areas. Further investigation could be completed to see how frequently these areas are attended by non-borough stations 
to identify if current provision is cost effective.

#### What factors predict a false alarm?
![image](https://github.com/tj2904/lfb-callout-analysis/assets/3164936/0f71ff17-321f-4165-a563-368990fbbdf7)

_More plots are in the [notebook](https://github.com/tj2904/lfb-callout-analysis/blob/main/LFB_Analysis.ipynb)_

It  is clear that false alarms are a key demand upon the resources of LFB, which suggests that any reduction in attending these 
would yield cost and service quality benefits. Models have demonstrated some ability to predict false alarms, but further 
work is needed to achieve the levels of accuracy that would be found acceptable. 

#### What factors are most associated with fires within dwellings?
It can be seen from the analysis that `PropertyType` is a factor that is associated with Fires within dwellings. 
Specifically, A property type of House – Single Occupancy, or Purpose Built Flats/Maisonettes are the most associated types. 
This is in-line with what intuition may suggest. It is also indicated that residential fires are more often associated with 
a low number of calls. What isn’t associated with Dwelling Fires is also, and potentially more so, interesting. For example, 
large multi-person dwellings such as tower blocks do not appear to be more likely to be the location of a dwelling fire.

## Summary
This section presents a summary of the findings along with recommendations for LFB.
It is suggested that LFB look into the false alarm rate at Chiswick as this is particularly high, proportionally, for the 
borough they also attend far fewer incidents, addressing this may support and improvement in the service.
The increase in the four wards maybe due to a rise in housing, identifying if this is the case, and reviewing existing plans 
for further housing expansion would support future service provision planning.
