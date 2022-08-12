RCA of Cliff &amp; Caruso 1998 <img src="man/figures/200px-Rti-logo.png" align="right" />
========================================================

RCA was developed by RTI International to implement the Reliable Component 
Analysis (RCA) of Cliff &amp; Caruso (1998).

## Installation

Go to [https://github.com/ICTatRTI/RCA/tags](https://github.com/ICTatRTI/RCA/tags)
and click on the top most `tar.gz` link to download the newest version of the `RCA` package.


In R, use

```
install.packages("path/to/RCA-0.1.0.tar.gz", repos = NULL, type = "source")
```

substituting the path where you saved the `tar.gz` file. 

## Replicate the analyses of Cliff and Caruso (1998)

### RCA R Package

```
library(RelComp)

# simulate data using the Cliff and Caruso (1998) correlation matrix
data(corr)
data <- corrSim(corr)
reliab <- c(.90, .89, .96, .86, .84, .82, .85, .76, .89, .68, .86)

# view the RelComp documentation
?RelComp

# run RelComp on the simulated data
output <- RelComp(data, names(data), reliab)

# view the reliabilities, compare to the first row in Table 8 of 
# Cliff and Caruso (1998)
round(output$reliabilities[1:5], 3)
```

### SAS

The following SAS files are available [here](https://github.com/ICTatRTI/RCA/tree/master/inst/SAS) 

* `RelComp.sas` which contains a SAS macro for producing reliable components.

* `RelComp Macro C&C 98 example.sas` which applies the SAS macro to the data of
Cliff and Caruso (1998).

* `RelComp Macro C&C 98 example.lst` which contains the output of the 2nd SAS file.


The user can verify that the `RCA` `R` package replicates the the analyses of 
Cliff and Caruso (1998) as well as the replication provided by the SAS files 
(within rounding), with one caveat: for some columns of the weight matrices
in the `R` results will have a different sign than those in the SAS output (i.e.,
the column is multiplied by -1). This reflects differences in the ways 
generalized eigen vectors and eigen values are calculated, but does not affect 
the estimated reliabilities (these will be the same, within rounding, between
`R` and SAS).

### Comparison of `R` and SAS results

#### SAS Reliability Estimates

See "\inst\SAS\RelComp Macro C&C 98 example.lst"

```
RCA component reliability estimates             
	
			       
Rel             Unrotated       
Component       reliabilties     

Component1        0.98296      
Component2        0.86056      
Component3        0.83266      
Component4        0.80298      
Component5        0.70776      
Component6        0.66565      
Component7        0.58705      
Component8        0.54399      
Component9        0.52484      
Component10       0.50356      
Component11       0.15473  
```

#### R Reliability Estimates

```
round(matrix(output$reliabilities),5)

Component1        0.98295
Component2        0.86053
Component3        0.83291
Component4        0.80303
Component5        0.70824
Component6        0.66516
Component7        0.58804
Component8        0.54383
Component9        0.52492
Component10       0.50280
Component11       0.15477
```


