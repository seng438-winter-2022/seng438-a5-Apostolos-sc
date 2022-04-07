**SENG 43[Lab5.pdf](https://github.com/seng438-winter-2022/seng438-a5-Apostolos-sc/files/8446416/Lab5.pdf)
8- Software Testing, Reliability, and Quality**

**Lab. Report \#5 – Software Reliability Assessment**

| Group \#3:            |   |
|-----------------------|---|
| Student Names:        |   |
| Apostolos Scondrianis |   |
| Josh Vanderstoop      |   |
| Haniya Ahmed          |   |
| Beau McCartney        |   |




































# Introduction

The purpose of this assignment is to help students familiarize themselves with tools that can help with analyzing the reliability of a system under test. A set of integration test data was provided to each team. This test data is used throughout this document in conjunction with two reliability analysis softwares. Specifically, C-SFRAT for Reliability Growth Testing analysis by performing model fitting with different combinations of hazard functions and covariates and using a Reliability Demonstration Chart (RDC) to check whether the target failure rate or MTTF is met or not.

A List of how covariates are referred in this document follows :

E: execution time measured in hours
F: failure identification work measured in person hours
C: computer time failure identification measured in hours

In order to select the range of data that we can use for reliability analysis, we decided to use the Laplace trend analysis

# Assessment Using Reliability Growth Testing 

Our team chose to use the RGT tool called C-SFRAT. We imported the failure data provided in the assignment. The provided hazard functions are IFR Salvia & Bollinger (IFRSB), IFR generalized Salvia & Bollinger (IFRGSB), S Distribution (S), Discrete Weibull (Order 2) (DW2), Discrete Weibull (Type III) (DW3), Geometric (GM), Negative Binomial (Order 2) (NB2) and Truncated Logistic (TL).
The software originally shows a plot of Total Cumulative Failures versus Time Interval :

















Figure 1: Total Cumulative Failures vs. Time Interval




First we run the 8 simulations using covariates E, F as the covariates :


Figure 2: Simulated RGT Models on Covariate Failure Data
Then we viewed the model comparison data provided by the software  : 









Figure 3: Model Comparison Data

The 5 criteria of interest are : the log-likelihood, the Akaike information criterion (AIC) and Bayesian Information Criteria (BIC) as well as sum of squares (SSE) and predictive sum of squares error (PSSE).
By looking at these 5 parameters we determine that IFRGSB is ranked as our number 1 most fitting model and then GM is #2. We picked GM as #2 by comparing S, GM, TL on AIC, BIC, SSE and PSSE. GM scored lower in 3 of those criteria. 

Isolating the two  models we can see that they closely follow the pattern of failures on the specified intervals : 

Figure 4: Isolated Best-Fit RGT Models

The software also allows us to view the models and data as failure intensity versus time. The following graph shows the data we imported.
The x-axis represents the failures on a specific interval and then the y-axis represents the time interval those failures occurred in.
















Figure 5: Failure Intensity Graph

Figure 6: Simulated RGT Models on Failure Intensity Graph

Figure 7: Isolated Best-Fit RGT Models
In order to choose our data range, we manually inputted our test data into the software called CASRE using a VM to run the software. Our results of Laplace trend testing can be seen in the following screenshots: 



















Figure 8: CASRE Laplace Test Results

From the Laplace test we observe for the test intervals 1 to 18 there is stable reliability and slight reliability growth. After that for the  interval of values 19 to 31 we observe stable reliability since the laplace test values are between 2 and -2 as we can see from the data and the plot. Since the Laplace test indicates fairly stable reliability with not too many extreme high number failures at random intervals it is fair to accept the whole range of provided data. 

A target failure rate can be used in reliability growth testing can be used to determine whether the high number of failures at the aforementioned random intervals results in the SUT being rejected or not. 

Reliability growth testing is advantageous as it allows for the estimation of system reliability improvement as a system undergoes testing, and allows the developer to view different failure modes. There are also a variety of different models available now, along with a variety of tools. However, it becomes difficult to utilize this form of testing to determine true reliability of a system since the failure modes occur randomly. There are, however, models that can smooth out system reliability estimates by accounting for the inevitable lack of predictability in test observation patterns. Another disadvantage of reliability growth models is that they do not necessarily account for previous fixtures of failures if new failures are found, say, in another test of the same system. 





# Assessment Using Reliability Demonstration Chart 

For assessing this hypothetical System Under Test we used the provided RDC excel spreadsheet. First, we substituted the demonstration data with the given data points, combining the time intervals in sets of two and accumulating the errors detected at that point. Then by selecting the first 5 data points to show on the graph, as described by the TA team during labs, we could begin to define the minimum acceptable threshold for system errors. The first point at which the system is acceptable is when a maximum of 40 errors are found through 32 time intervals, the next steps are to set the MTTFmin to twice the original value, and then half of the original value; these plots are shown below, respectively. 

Figure 9: Minimum MTTF


Figure 10: Twice the Minimum MTTF 



Figure 11: Half the Minimum MTTF 

What is evident in these plots is that as the acceptable number of failures increases, the program becomes more acceptable for use, and as the MTTF decreases, the program must be rejected for the amount of failures that occur during the runtime. This is reasonable considering that the MTTF is a measurement of the overall time that a system runs, divided by the number of failures or defects. 

In order to determine the minimum MTTF, we tested the failure data with different MTTF values until we arrived at a plot where the last failure data was just hardly crossing into the accepted plot range, as seen in Figure 9.

The advantage of using RDC to determine the reliability of an SUT is that it allows both the customer and developer to determine the acceptable failure rate for a system. With RDC, the failure data is easily visualized in comparison wih the acceptable and rejectable failure targets. Furthermore, once used to the tools, RDC is a very fast and cost-efficient way of determining the reliability of an SUT. However, one disadvantage noticed in this lab is that the MTFF minimum requires a little more good guess-work, but the visualization of the chart definitely assists in arriving at the assumed MTTF minimum, despite being tedious. It also shows reliability in terms of relativity and trend rather than providing a quantitative value. 

# Comparison of Results

Both the Relaibity Growth Testing and Reliability Demo Chart yielded in a consensus that the SUT is reliable given the failure data. Although failure intensity does spike in some intervals, the overall system remains reliable, and all the failure data remains usable. 

# Discussion on Similarity and Differences of the Two Techniques

There are some similarities and differences that we noticed between the Reliability Growth Testing and the Reliability Demo Chart. Both techniques seemed to arrive at the same conclusion, but most importantly, both had results that were based on inter failure times and target failure intensity (MTTF). However, RDC definitely allowed for more visual aid than RGT. Furthemore, both techniques are cost and time efficient. Although, RGT provides more quantitative data that can be measured with concrete values, RDC provides a trend analysis of the reliability of the SUT relative to the constraints of acceptable and rejectable data. As such, RGT has less tedious guess-work when attempting to arrive at the MTTF value. Also, RGT measures improvements in reliability along with measuring what data is usable. 

# How the team work/effort was divided and managed

Haniya and Apostolos worked on the first part of the lab assignment together. They worked on figuring out how to use the tools such as CSFRAT, CASRE and SRTAT. They successfully figured out how to use CASRE for by installing a Virtual Machine for DOS and running CASRE and manually inputting our data points. They then ran the laplace tests and chose the acceptable data range. In order to find which reliability model is best to fit with the provided data they used the tool CSFRAT. They ran several simulations and provided the charts and analysis on why the IFR Salvia & Bollinger (IFRSB) and Geometric (GM) models fit best the provided test data. Josh and Beau worked on the second part of the lab assignment together and attempted using both SRTAT and the provided Excel sheet to determine an RDC model for the provided failure data. They were able to adjust the data in the Excel file according to the provided failure data, specifically the cumulative failure counts, to produce an RDC. They adjusted the chart variables to determine the minimum MTTF, scaled the demo chart, and scaled the boundaries to arrive at accurate results of the data. 



# Difficulties encountered, challenges overcome, and lessons learned

Even though the concepts were not hard, it was very challenging to figure out how to get each tool to work. CSFRAT was the easiest of all to use and most straightforward. SRTAT was even more challenging as the RDC functionality was not working and we had issues on getting the tool to model using our data. CASRE would be the recommended tool to use in order to perform the laplace test, but I would suggest to the TA’s if they use CASRE again to give clear instructions on how to use it for La Place testing. The RDC tool is also very hard to use. There are no clear instructions provided by the user manual. There was an overview of 1 page and that was it. The team learnt that you can not give up and keep trying until you get an acceptable result. Sometimes your efforts do not reflect the result and that is okay.

# Comments/feedback on the lab itself

Overal, this was perhaps that trickiest lab for all group members. Although a variety of tools were provided in order to complete the lab, the tools lacked in thorough instruction of how to operate the tool using the failure data. It was definitely a struggle to determine how to not only input the data in the format required, but also achieve the desired output, amongst many other struggles. 

A few quick comments on the lab :
For CASRE tool, let people know how to run the tool.
First install the virtual machine by running DOSBoxinst.exe :











Second step : Run inst.bat

Step 3 : Running CASRE 

Quick note, do the data inputting directly through the VM as in some machines the Virtual Box and the System files do not update after you are done using the VM or even won’t read files added in the VM system folder (new ones). There is some sort of caching that is done the leads to unexpected behavior.
Instead : run the built in notepad :














And manually input the information in the following format : 


This info was taken from page 192/220 of the user manual or ~180 of the original paper manual.










