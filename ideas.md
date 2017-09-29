This document is designed to help you think of ideas for course content. Don't worry about the order of the ideas, or how stupid they are. (Filtering and ordering comes later.) Just write down anything that might be interesting.

### What problems do you want the student to be able solve?

*For example:*   
*How to draw plots using ggplot2.*  
*How to run a random forest model.*  
*How to analyze data from a clinical trial.*  
*How to forecast the demand of a product.*  



### What techniques or concepts do you want students to learn?

*For example:*  
*Combining plot elements using `+`.*  
*The split-train-model-predict modeling workflow.*  
*Type I vs. Type II errors.*  
*Start with Holt-Winters models and work up to time-based neural networks.*  



### What technologies, packages, or functions do you want them to use?

*For example:*  
*`ggplot2` for drawing plots and `dplyr` for manipulating the data.*  
*Focus on `caret` and `ranger` but discuss the Rborist and `randomForest` pkgs as alternatives.*  
*Use `experiment` for experimental design. Not sure whether to use `pwr` or `PwrGSD` for sample size calcs.*  
*Mainly `forecast` but might need to discuss `xts` for the time series.*  



### What terminology or jargon will you need to define?

*For example:*  
*All the grammar of graphics terms like aesthetics and geoms.*  
*Boosting vs. bagging, different types of cross validation (k-fold, Monte Carlo, etc.).*  
*Type I/II, RCT = "randomized clinical trial", compare block/factorial/sequential designs.*  
*Forecasting vs. prediction, "Seasonal adjustment" "rolling statistics".*  



### What analogies can you use to explain concepts?

*For example:*  
*ggplots are like Lego for graphics.*  
*Random forests are like a parliament of decision trees.*  
*http://marginalrevolution.com/marginalrevolution/2014/05/type-i-and-type-ii-errors-simplified.html*  
*Seasonality and trends are like revolution and evolution respectively.*  



### Are there any heuristics to help students understand things?

*For example:*  
*Draw simple plots then adding elements one by one.*  
*Split the dataset into 70% training, 30% testing.*  
*For factor analysis with 10 items, the sample size should be at least 200 (https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2447286)*  
*Don't use Holt-Winters if your demand spikes on holidays.*  


### Are there any potential pitfalls that you want to help students avoid?

*For example:*  
*Changing colors, etc., works differently if the color arg is inside an aesthetic or not.*  
*Overfitting models to the dataset.*  
*Confusing sensitivity and spcificity.*  
*Extrapolating too far into the future.*  



### What datasets to you want to include in the course?

*For example:*  
*Anything but the diamonds and mtcars datasets.*  
*Somethings from the UCI Archive (http://archive.ics.uci.edu/ml/index.php), probably 1 dataset per chapter.*  
*An infectious disease example (flu?), and something heritary, probably from https://ndar.nih.gov/data_from_papers.html*  
*The Dominick's Finer Foods dataset (https://research.chicagobooth.edu/marketing/databases/dominicks/dataset.aspx)*  



### Is there anything else you want to include?







