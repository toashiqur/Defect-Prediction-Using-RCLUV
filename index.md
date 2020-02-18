The replication package: **Defect Prediction Using RCLUV.7z** contains the bug datasets needed to replicate our study. It also has the RCLUV extractor for Java. The datasets were built from two existing benchmark bug datasets: the Eclipse bug dataset (https://ieeexplore.ieee.org/abstract/document/4273265) and the GitHub bug database (https://link.springer.com/chapter/10.1007/978-3-319-42089-9_44).

The thesis is available for download from: (http://hdl.handle.net/1974/27517)

# Overview of the Replication Package Content
<html>
<dl>
  <dt>|-RCLUVExtractor</dt>
  <dd>It contains the programs needed to extract the RCLUVs of source files.</dd>  
  
  <dt>|-Eclipse</dt>
  <dd>
    <dl>
      <dt>|--Eclipse_RCLUV</dt>
      <dd> It has three *.RcluvAnalysis.csv files and one titles.txt file. These files were generated using the RCLUV extractor on Eclipse source files. These files do not contain the feature column names. They can be found in the titles.txt file. However, in addition to RCLUVs the *.RcluvAnalysis.csv files have two non-RCLUV columns: file path, and counts of number of lines. From these files we removed TXL warnings generated during feature extraction.</dd>
      <dt>|--Eclipse_filename_bug_RCLUV</dt>
      <dd>It has six files- three *_rcluv_bug.csv and three *_rcluv_bug.arff files. These files have the column titles. The *_rcluv_bug.csv files contain Project, Version, Class and isBuggy columns in addition to RCLUV element columns of each source file. The *_rcluv_bug.arff files contain isBuggy and the RCLUV elements.</dd>
      <dt>|--Eclipse_Results</dt>
      <dd>It has two result files Comparison_with_choudhary.xlsx and Comparison_with_Zimmermann.xlsx </dd>
    </dl>
  </dd>
  
  <dt>|-GitHub</dt>
  <dd>
    <dl>
      <dt>|--GitHub_RCLUV</dt>
      <dd>It has fifteen *.RcluvAnalysis.csv files and one titles.txt file. These files were generated using the RCLUV extractor on Eclipse source files. These files do not contain the feature column names. They can be found in the titles.txt file. However, in addition to RCLUVs the *.RcluvAnalysis.csv files have two non-RCLUV columns: file path, and counts of number of lines. From these files we removed TXL warnings generated during feature extraction.</dd>
      <dt>|--GitHub_filename_bug_RCLUV</dt>
      <dd>It has thirty files- fifteen *_rcluv_bug.csv and fifteen *_rcluv_bug.arff files. These files have the column titles. The *_rcluv_bug.csv files contain Project, Version, Class and isBuggy columns in addition to RCLUV element columns of each source file. The *_rcluv_bug.arff files contain isBuggy and the RCLUV elements. </dd>
      <dt>|--GitHub_Results</dt>
      <dd>It has eight files. Fore each particular classifier the *.all_models_avg.xlsx files contain the 10 fold cross validation results of 10 randomly undersampled subsets of the datasets. Compare_with_Toth.xlsx compares the performance of RCLUV-based models with product metrics-based models. Voting_performance.xlsx gives the performance of majority voting classifiers for each project. Individual vs Voting performance.xlsx compares the performance obtained using a single classifier and a voting classifier for each project.
      </dd>
    </dl>
  </dd>
  
  <dt>|-ReadMe.txt</dt>
  </dl>
  </html>
  
# Running the RCLUV Extractor
The RCLUV extractor is written in [TXL][txl-link]. You need to have it installed on your machine.
  
# Replication of the Study
In our [report][thesis-link] we published the performance of the models developed using the [WEKA][weka-link] machine learning tool. We used WEKA version 3.8. The \*.arff data files provided in *Eclipse\Eclipse_filename_bug_RCLUV\\* and *GitHub\GitHub_filename_bug_RCLUV\\* can be used to train machine learning models in WEKA with the minimum effort.

## Hyperparameters
  Below we present the hyperparameters that were used to develop the models.
  
### Eclipse
![]({{site.baseurl}}/assets/images/hyper_param_learning_curve.png "Hyperparameters of the models used to plot the learning curves for the Eclipse bug dataset")
*Table.1 - Hyperparameters of the models used to plot the learning curves for the Eclipse bug dataset*

![]({{site.baseurl}}/assets/images/hyper_param_training_time.png "Hyperparameters of the models used to measure the training time for the merged Eclipse bug dataset")
*Table.2 - Hyperparameters of the models used to measure the training time for the merged Eclipse bug dataset*

![]({{site.baseurl}}/assets/images/hyper_param_with_cost_eclipse.png "Hyperparameters with cost matrix used to develop models for the Eclipse bug dataset")
*Table.3 - Hyperparameters with cost matrix used to develop models for the Eclipse bug dataset*

![]({{site.baseurl}}/assets/images/hyper_param_with_cost_github.png "Hyperparameters used to develop models for the GitHub bug database")
*Table.4 - Hyperparameters used to develop models for the GitHub bug database*

## Feature Extraction
The *RCLUVExtractor* directory contains a script **AnalyzeRCLUV.sh**. It takes a java directory name as its argument, and finds all the \*.java files from the given directory. After extracting the RCLUVs of the source files it generates a \*.RCLUVAnalysis.csv in the parent directory of the give project directory. The extractor writes any errors or warnings triggered during the feature extraction process to the result file. The AnalyzeRCLUV.sh script should be invoked using the following command.

```
./AnalyzeRCLUV.sh Java_directory
```
Below we use the above command on the source files of *examples/java* directory provided with the RCLUVExtractor.
```
rahman@MSI-GP62-6QF:~/Downloads/RCLUVExtractor$ ./AnalyzeRCLUV.sh examples/java
Compiling 
.....................................................................................Done.
```
It generates a java.RcluvAnalysis.csv file inside the directory *examples/*

## Feature Titles
The titles of the feature columns aree needed to be generated separately using the following command.
```
txl -q -s 1000 dummy.java rcluv-java.txl -d SPREADSHEET -d TITLES 2> titles
```
We run the above command replacing the *dummy.java* placeholder with the path of a java file as shown below.
```
rahman@MSI-GP62-6QF:~/Downloads/RCLUVExtractor$ txl -q -s 1000 examples/java/Policy.java rcluv-java.txl -d SPREADSHEET -d TITLES 2> titles.txt
```
It generates a titles.txt file inside the *RCLUVExtractor* directory.


[thesis-link]:http://hdl.handle.net/1974/27517
[weka-link]:https://www.cs.waikato.ac.nz/ml/weka/
[txl-link]:https://www.txl.ca/
