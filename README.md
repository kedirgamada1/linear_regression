# linear_regression
*The dataset is taken from SasHelp library;
*The objective of this code is to create a linear regression model;

data work.from_sas;
	set sashelp.heart;
run;

* Exploring work.from_sas;

proc contents data=from_sas;
run;

proc means data=from_sas max min mean n;
	var weight systolic;
run;

proc means data=from_sas nmiss;
	* Needs to be fixed;
	var weight systolic;
run;

proc freq data=from_sas;
	table diastolic systolic / nocum nopercent;
run;

ods graphics on;

proc sgscatter data=from_sas;
	plot diastolic * systolic;
run;

ods graphics on;

proc univariate data=from_sas;
	histogram diastolic;
run;

quit;
ods graphics on;

proc univariate data=from_sas;
	histogram systolic;
run;

quit;

proc sgplot data=from_sas;
	hbox systolic;
run;

proc sgplot data=from_sas;
	hbox diastolic;
run;

*Scatter plot with regression line.;

proc sgplot data=from_sas;
	scatter x=systolic y=diastolic;
	reg x=systolic y=diastolic;
	title "Systolic vs. Diastolic" run;
	*Examining correlation among four variables;

proc corr data=from_sas;
	var systolic diastolic height weight;
run;

*Running proc reg with and model to get the parameter;
ods graphics on;

proc reg data=from_sas;
	model systolic=diastolic;
	run;
	*Writting a model;
	systolic=diastolic * 1.45672 + 12.56597 * Let us predict using the regression 
		model.;
	* A person with a diastolic of 75 approximatly will have a systolic of 122;
	*ststolic = 75 * 1.45672 + 12.56597
*systolic ~= 122;
	*Interpretation;
	*For one unit increase in diastolic we can expect 1.45672 unit increase in systolic keeping other things constant.;
