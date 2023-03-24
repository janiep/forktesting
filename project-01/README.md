--- 

# Project 1: Standardized Testing Analysis
# Syndey is very cool!
--- 

## Executive Summary

### Contents:
- [Problem Statement](#Problem-Statement)
- [Description of Data](#Description-of-Data)
- [Conclusion & Recommendations](#Conclusion-&-Recommendations)
- [Next Steps](#Next-Steps)

### Problem Statement

This project aims to explore trends in SAT participation from 2017-2019.

Today, some states require students to take the SAT as a graduation requirement. 
The state of South Carolina is talking to an employee at the College Board and is wondering, if the state were to implement a requirement for SAT test participation, what effects would these requirements have on the school. Due to the increased participation, the state is worried that their scores will be dropped and is questioning if implementing this will be advantageous.


South Carolina currently does not require the participation of the SAT or ACT, but provides both exams to juniors at no cost ([*source*](https://blog.collegevine.com/states-that-require-sat/#curve)).

### Description of Data

#### Size
From the 3 sources below, I created a dataset [`combined_sat_years.csv`](.data/combined_sat_years.csv) which combines SAT data from 2017, 2018, and 2019 and features the state, participation, evidence-based reading and writing, and math scores for each year.

The size of the dataset is 51 rows and 13 columns.

#### Source
Provided from the project-01-main README.md page:
- [`sat_2017.csv`](./data/sat_2017.csv): 2017 SAT Scores by State ([source](https://blog.collegevine.com/here-are-the-average-sat-scores-by-state/))
- [`sat_2018.csv`](./data/sat_2018.csv): 2018 SAT Scores by State ([source](https://blog.collegevine.com/here-are-the-average-sat-scores-by-state/))
- [`sat_2019.csv`](./data/sat_2019.csv): 2019 SAT Scores by State ([source](https://blog.prepscholar.com/average-sat-scores-by-state-most-recent))

#### Target
Target is a regression analysis.

#### Data Dictionary
|Feature|Type|Dataset|Description|
|---|---|---|---|
|state|object|sat_2017, sat_2018, sat_2019|Name of states participating in the SATs.|
|participation_2017|float|sat_2017|Participation rate of test takers from each state in 2017. (unit is converted to a decimal)|
|evidence_based_reading_writing_2017|integer|sat_2017|Mean number scored on the evidence-based reading and writing portion of SAT per state in 2017.|
|math_2017|integer|sat_2017|Mean number scored on the math portion of SAT per state in 2017.|
|total_2017|integer|sat_2017|Total score from evidence_based_reading_writing and math in 2017.|
|participation_2018|float|sat_2018|Participation rate of test takers from each state in 2018. (unit is converted to a decimal)|
|evidence_based_reading_writing_2018|integer|sat_2018|Mean number scored on the evidence-based reading and writing portion of SAT per state in 2018.|
|math_2018|integer|sat_2018|Mean number scored on the math portion of SAT per state in 2018.|
|total_2018|integer|sat_2018|Total score from evidence_based_reading_writing and math in 2018.|
|participation_2019|float|sat_2019|Participation rate of test takers from each state in 2019. (unit is converted to a decimal)|
|evidence_based_reading_writing_2019|integer|sat_2019|Mean number scored on the evidence-based reading and writing portion of SAT per state in 2019.|
|math_2019|integer|sat_2019|Mean number scored on the math portion of SAT per state in 2019.|
|total_2019|integer|sat_2019|Total score from evidence_based_reading_writing and math in 2019.|

The features most prominent in the final model are the state, participation_2017, total_2017, participation_2018, total_2018, participation_2019, and total_2019.

- state: This feature is an object taken from all 3 datasets. It provides the name of states that are participating in the SATs. There are 51 states included.
- participation_2017: This feature is a float and is derived from the dataset [`sat_2017.csv`](./data/sat_2017.csv). It provides the participation rate of SAT test test takers from each state in 2017 (units is converted to a decimal).
- total_2017: This feature is a float and is derived from the dataset [`sat_2017.csv`](./data/sat_2017.csv). It provides the mean total score from the evidence based reading and writing and math section of the SATs in 2017.
- participation_2018: This feature is a float and is derived from the dataset [`sat_2018.csv`](./data/sat_2018.csv). It provides the participation rate of SAT test test takers from each state in 2018 (units is converted to a decimal).
- total_2018: This feature is a float and is derived from the dataset [`sat_2018.csv`](./data/sat_2018.csv). It provides the mean total score from the evidence based reading and writing and math section of the SATs in 2018.
- participation_2019: This feature is a float and is derived from the dataset [`sat_2019.csv`](./data/sat_2019.csv). It provides the participation rate of SAT test test takers from each state in 2019 (units is converted to a decimal).
- total_2019: This feature is a float and is derived from the dataset [`sat_2019.csv`](./data/sat_2019.csv). It provides the mean total score from the evidence based reading and writing and math section of the SATs in 2019.


### Conclusion & Recommendations

#### Conclusion
In general, participation within the years 2017 and 2019, has seen a slight upward trend in participation. Percentage in participation is also either heavily low (approximately 10% or lower) or high (approximately 90% and above). Only 3 states, Connecticut, Delaware, and Michigan had 100% participation throughout the 3 years.

Participation in 2017 is positively correlated to participation in 2018 (+0.87) and 2019 (+0.84). This correlation is expected because we would not expect participation rates to drastically change within each year.

Total SAT scores in 2017 are positively correlated to total scores in 2018 (+0.85) and 2019 (+0.90). This correlation is also expected because we are looking at only a change in one year and scores would not drastically change.

For participation and total mean score between years 2017 and 2019, there is a strong negative correlation. This means that as participation rates go up, the average score will go down. This makes sense because if there is an increase in the amount of students taking the test (who may not willingly be inclined to), scores may drop. In comparison, lower participation levels where only students who are serious about taking the SATs are taking the test and therefore, scores may be higher.

Although there is a negative correlation, it may not be drastic enough to outweigh the benefits of equal education, accountability for teachers, streamlined standardized testing.

#### Recommendations
South Carolina:
I recommend that an SAT School Day should be mandated in South Carolina. An SAT School Day helps establish equality in participation within the school because the test will be taken on a weekday during school hours at the same school ([*source*](https://collegereadiness.collegeboard.org/sat/k12-educators/sat-school-day/about#:~:text=SAT%20School%20Day%20provides%20schools,accepted%20at%20all%20U.S.%20colleges)). Earlier we saw that participation for the SAT is either heavily low or heavily high. South Carolina's participation was 50% in 2017 and steadily increases to 55% and 68% in 2018 and 2019. By having an SAT School Day, the College Board will be able to help improve the participation that is already increasing in the state, while also making sure the mean scores aren’t decreasing. If schools were to mandate an SAT School Day, schools could also utilize the SAT as a replacement to other state standardized testing. This would "streamline standardized testing by eliminating other 'unnecessary' exams, increase access to the SAT, particularly for lower-income students and inspire some students to apply to college" ([*source*](https://blog.collegevine.com/states-that-require-sat/#curve)).

Because the state already pays for the students to take either the ACT or SAT, I believe it would be advantageous to put those resources into one test so that the state can utilize the SAT as their state's overall standardized testing. By only paying for one test, the state can also put more effort into the test and potentially increase student SAT scores.

Overall Recommendation:
- Work with state boards to increase and promote SAT School Days and potentially making the SAT a graduation requirement so that students have a greater incentive to show up
- Promote utilizing the SAT as a replacement for any other state standardized test

### Next Steps

To further investigate this problem statement and to go into more detail, I think it would be interesting to compare just the evidence-based reading and writing portion and the math portion separately. I also think it would be important to not look at just 100% participation rates, but to take a look further into why the histogram shows an inverted bell shaped curve and why that may be by looking further into states within the lower part of the histogram.

Yes, this project demonstrates skills that can be applied to similar problems.
