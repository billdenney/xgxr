# xgxr

[![license: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](https://opensource.org/licenses/MIT) [![Travis build status](https://travis-ci.org/Novartis/xgxr.svg?branch=master)](https://travis-ci.org/Novartis/xgxr)

The xgxr package supports a structured approach for exploring PKPD data ([outlined here](http://opensource.nibr.com/xgx)).  It also contains helper functions for enabling the modeler to follow best R practices (by appending the program name, figure name location, and draft status to each plot).  In addition, it enables the modeler to follow best graphical practices (by providing an xgx theme that reduces chart ink, and by providing time-scale, log-scale, and reverse-log-transform-scale functions for more readable axes).  Finally, it provides some data checking and summarizing functions for rapidly exploring a PKPD dataset.

## How to update/test/use package
* **Developing the package:** Run [_Package_Setup.R](_Package_Setup.R).  This will update the documentation, reinstall the package, and rebuild the vignette.
* **Installing the package for use in your project:** follow the directions below, also [here](_Package_Install_New_User.R).  There are a few options.
  * **Option 1:** Install directly from Github to a local repository with the following command: `devtools::install_github("Novartis/xgxr", args = c('--library="./"'))`.  If you want to install it in your default library path, you can delete the "args" option.
  * **Option 2:** Download the package as a zip file and build and install it yourself, following the directions below.
    * Download this package as a zip file
    * Place the zip file in your project folder, with your R code. (if you don't have a project folder, then create one)
    * Unzip the file.  
    * Open R 
    * Set the working directory to your project folder.
    * Type: `devtools::build("xgxr-master")` (if you don't have devtools, install that first using command: `install.packages("devtools")`)
    * Then type: `install.packages("xgxr-master", repos = NULL, lib = "./", type = "source")`
    * To load the package, type: `library(xgxr, lib.loc = "./")`
  * **Option 3:** Source the R files and read in the data files directly
    * Download this package as a zip file
    * Place the zip file in your project folder, with your R code. (if you don't have a project folder, then create one)
    * Unzip the file.  
    * Open R
    * Execute the following code:
      ``` 
      Rfiles = list.files(path = "xgxr-master/R/", full.names = TRUE)
      for(ifile in Rfiles) {
        source(ifile)
      }
      
      Rdafiles = list.files(path = "xgxr-master/data", full.names = TRUE)
      for(ifile in Rdafiles) {
        load(ifile)
      }
      ```
  * **Last Resort Failsafe:** If you want to copy code from xGx exploratory graphics webpage but are unable to install the  `xgxr` package, you can use an older version of the website that does not make use of the `xgxr` package.  http://opensource.nibr.com/xgx_v1
  
## Your contribution
* If you will be helping to contribute, we make an effort to follow the [tidyverse style guide](https://style.tidyverse.org/index.html).

## Overview for how R packages (including this one) are organized

### Functions
Functions are located in the "R" folder.  
* When creating a new function, copy an existing one and follow the same format, with the documentation in the header
* When creating a new function, make sure to also add example code and some code to the vignette.
* For the function to be visible after the package is loaded, make sure to have the @export line.  

### Datasets
Sample datasets are stored in the the data folder as ".Rda" files and also, for convenience, in the inst/extdata folder as csv files.  Code for generating some of these datasets is stored in the data_create folder.  And the Single Ascending Dose PKPD dataset came from [https://github.com/dpastoor/PKPDdatasets/blob/master/R/PKPDdatasets.R#L31]

### Documentation
Documentation is located in the "man" folder.  Do not edit this folder.  Instead, edit the documentation within the function header and the documentation will be automatically created [as described here] (https://cran.r-project.org/web/packages/roxygen2/vignettes/roxygen2.html).

### Vignettes
Vignettes are documents that show how a package can be used.  They are located in the "vignettes" folder.  Build them using the devtools::build_vignettes() function.

### Description files
* The DESCRPTION file is where you list the dependencies on any other packages.
* The NAMESPACE file lists which packages are exported.  It should not be edited because it's automatically generated by the devtools::document() command

## Here are some links for learning more about packages
* [Hilary Parker's brief intro](https://hilaryparker.com/2014/04/29/writing-an-r-package-from-scratch/)
* [Hadley Wickham's book](http://r-pkgs.had.co.nz/)
* [Developing package with Rstudio](https://support.rstudio.com/hc/en-us/articles/200486488-Developing-Packages-with-RStudio)
* [Getting a package onto CRAN](https://cran.r-project.org/web/packages/policies.html)

## Scope of the project
* Base case (100%)
    * Helper functions - log scale, confidence intervals, etc. [DONE]
    * Vignettes that show idea and work with examples in nlmixr/ggpmx [pk-DONE, pd-DONE]
    * Data checking: xgx_check_data() - [DONE]
* Under Consideration (50%)
    * Overview Plots: xgx_explore_pk(data,units), xgx_explore_pd, xgx_explore_pkpd [CONSIDERING]
      * (continuous, binary, RO)
      * repeated time to event
      * We still need to align as a team on whether we want to provide this functionality, or just have the user copy the Rmarkdown documents from the vignettes or https://opensource.nibr.com/xgx.  The advantage of this functionality is that it makes some plots even easier to create.  The disadvantage is that it's more functions for the user to learn and more work to maintain the package and many of the commonly used plots can be created with just a few lines of code.
* Stretch goal (40%)
    * Additional datatypes [TO DO]
      * RECIST (Target, Nontarget, and New lesions), 
      * Liver enzymes (ALT, AST, Bilirubin, etc.)
      * Blood counts (Neutrophils, Platelets, Blasts).

## Roadmap
* Continue coding
    * Finish base case at minimum, and possibly some additinoal functionality.
* Begin process of "validation" for CRAN and put version 1 onto CRAN.
See [https://kbroman.org/pkg_primer/pages/cran.html]
  * From Rstudio, run `devtools::check()`
      * Alternatively one could navigate to directory containing package and type: `R CMD build ./`  
      * This will create a .tar.gz file (e.g. `xgx_0.0.1.005.tar.gz`)
      * Then, type: `R CMD check xgx_0.0.1.005.tar.gz --as-cran`
      * The devtools::check() above does the same thing (I think)
* Request installation on Novartis systems.
