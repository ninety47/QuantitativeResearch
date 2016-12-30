#Expectancy Dynamics
First released in @PipMeUp's expectancy mangement thread this scripts explore the dynamics of various and levels of expectancy.

##Model Constraints and assumpitons
- Risk is fixed.
- Reward is variable.
- Each trade is independent of the trade before it.

The risk is set at 1% by default but the actual size of the risk used in practive will only affect the gradient of the equity curves and not the overall dynamics. 
The variable reward, or payoff, is simulatted by sampling from the a distribution generated from minimum, maximum and mean values supplied to the simulaiton function. Its assumed that the pay off is normally distributed with a skew to towards smaller than larger payoffs e.g. you won't pull large winners consistantly but they do happen. It also can be considered an low-fi way to model trailing stops, targets that are set by abitrary goals e.g. 2 times risk, and trades that get cut because they are wrong (or have demonstrated good reasons to stop).
The final assumption that the trades are independent of each does disregard trader psycology but simplifies the modelling and keeps us focused on the task at hand - exploring the impact of expectancy and risk/reward payoff on the equity curve.

##Short-coming
The model doesn't stop trading if equity goes negative - this keeps the code simpler and helps to illustrate the equaity curve dynamics better in the plume plot.


##Running the script
On Linux simply execute the run script:

```
$ ./run.sh
```

Outputs are stored in a sub folder called "output". The BASH runner script will archive existing non-empty output folders.

On Windows you can execute the script either from with in the R GUI or R Studio by sourcing the file, for example:
```
> source('C:\\Scripts\\QuantitativeResearch\\Expectancy\\expectancy.R')
```
You will have to managed the outputs yourself.

##Outputs
There are 5 outputs from each simulation run:
- equity curve plume plot
- histogram of expectancy values across the simulated trades.
- histogram of the pay off distribution
- a CSV file of the data behind the plume plot
- a CSV file of the expectancy values for each simulation step.


###Equity curve plume plot
![alt text][img_plume_plot]
The plume plot shows the range of all the equity curves generated by the simulation (the grey plume in the plots background. The green and dark red lines represent the best and worst curves generated by the simulation. The dashed blue line represents average equity curve for all simulation runs. Positive growth the average line is a good thing.

###Expectancy histogram
![alt text][img_expectancy_hist]
Derived from the simulations the histogram shows the variance in the expectancy across all the simulations. The vertical green lines denote 1 and 2 standard deviations less than the mean. The help illustrate that with sufficient pay-off systems with expectancy rates bellow 51% have the potential to be profitable (specifically if 2 standard deviations below the mean is still positive).

The data in this plot can found in the ```"experiment_name"_expectancies.csv``` file.

###Sample pay-off histogram
![alt text][img_payoff_hist]
The generated sample of the potential payoffs used for each of trade in the simulation run. Presented as a diagnostic tool to verify we had the desired distribution in pay-offs. 

[img_plume_plot]: ./equitycurves.png "Equity curve plume plot"
[img_expectancy_hist]: ./expectancy_hist.png "Expectancy histogram"
[img_payoff_hist]: ./payoff_hist.png "Sampled payoff histogram"
