# Horse_colic-data-analysis
# 1.	Dataset

The project will be performed on the horse_colic dataset. The multivariate dataset is available in the form of .txt format as well as in .csv format. The dataset comes with 300 instances and 28 attributes, which are continuous, discrete, and nominal in nature. This dataset also comprises of around 30% missing values. The source for the dataset is UCI Machine Learning Repository. the target variable is the outcome and has three distinct classes, hence this is a multiclass classification problem, and hence the task associated is to predict or classify the instances, whether or not a horse can survive based upon past medical conditions.

Dataset Description: 
The attribute information for the given dataset is as follows:

<img width="702" alt="Screen Shot 2022-06-17 at 12 33 11 PM" src="https://user-images.githubusercontent.com/42109704/174339712-219eca89-8c1b-4998-a467-da02e9a84b24.png">


# 2. Dataset study and preprocessing

<img width="849" alt="Screen Shot 2022-06-17 at 12 35 03 PM" src="https://user-images.githubusercontent.com/42109704/174339983-da32f79e-a782-4488-aff9-241a9adc79b6.png">



# c. Problem identification


Observing for presence of target variable is necessary to identify whether the problem is supervised/ unsupervised machine learning and the type of target numerical or categorical to know if its regression or classification. Here outcome is the target variable and it has three levels, to show what eventually happened to a horse, whether 1: it lived, 2 : it died, 3: was euthanized. Hence the target variable makes this a supervised multiclass classification problem.
<img width="181" alt="Screen Shot 2022-06-17 at 12 35 58 PM" src="https://user-images.githubusercontent.com/42109704/174340107-d8e71360-df6a-449b-ba36-c08eca750732.png">


# d. Observing unique values per column

Here we can observe that there are multiple columns with an invalid data entry as ‘?’, which can be interpreted as unknown data. Our best option would be to replace these data entries using np.nan.
<img width="877" alt="Screen Shot 2022-06-17 at 12 36 28 PM" src="https://user-images.githubusercontent.com/42109704/174340161-2d731244-397d-46eb-9c10-9ae492ca7127.png">

**Using the command “df.replace(‘?’, np.nan,inplace=True)”, replace the “?” with “NaN” value, which is further reflected in the dataframe.
**


# e. Observation of datatypes and correction

It can be observed from information , datatypes, unique values per column, by default, only 7 columns are numerical datatype given by int64, and the rest 21 are ‘object’ type.
<img width="689" alt="Screen Shot 2022-06-17 at 12 37 20 PM" src="https://user-images.githubusercontent.com/42109704/174340301-26734526-3c7a-424f-b740-e6cee96c88c7.png">


# f. Splitting as numerical and categorical columns.

This splitting is necessary for proper treatment of missing values, by deciding the imputation strategy based on the datatypes.
<img width="625" alt="Screen Shot 2022-06-17 at 12 38 02 PM" src="https://user-images.githubusercontent.com/42109704/174340417-827fcfab-d2d2-4c6e-9b3f-0d2312a18406.png">


# g. Treating invalid values

From observing unique values, and study of dataset description it is found that the ‘age’, column, has an anomaly or invalid data. The’Age’ column is supposed to have only 1 and 2 classes, class 9 looks like a fault entry, hence replacing, all ’9’ with ‘2’, and then reverifying that the datatype remains ‘object’, else correct it.

<img width="905" alt="Screen Shot 2022-06-17 at 12 38 27 PM" src="https://user-images.githubusercontent.com/42109704/174340476-d8997fb6-cc61-4007-b7f5-728573199a51.png">


# h. Dropping Redundant Columns
<img width="882" alt="Screen Shot 2022-06-17 at 12 38 38 PM" src="https://user-images.githubusercontent.com/42109704/174340505-f9ee61e4-e551-4f5d-aafb-e5a159a28e34.png">



# i. Treatment of missing values i. Dropping columns

The three columns ('nasogastric reflux PH' (82%),'abdomcentesis total protein'(66%),'abdominocentesis appearance'(55%)), have more than 50% missing values. such columns, can hardly provide any insight, and if imputed can introduce bias, so dropping these columns.

**ii. Imputation **

The imputation is performed by using the simple imputer. We use the median strategy for replacing missing numerical values , as median is unaffected by outliers if present any. This is because mean is highly influenced by outliers.


# j. Statistical Analysis

Statistical information about categorical column, provides, count of valid datapoints, no.of unique levels/ classes, mode or most frequent class, and frequency of the mode class. The statistical information about numerical columns provides details like the total of valid entries, mean, standard deviation, minimum, maximum, and the Q1, Q2, Q3 values with regards to each numerical columns. We can analyse from high std deviation, huge difference from 75% and maximum, value etc as indicators of outliers. The statistical information on num_df shows presence of outliers.

<img width="600" alt="Screen Shot 2022-06-17 at 12 40 33 PM" src="https://user-images.githubusercontent.com/42109704/174340781-f0726932-0403-4a17-80c9-48b2a8012d02.png">


# k. Detection and Treatment of Outliers

The outliers are well evident from the box plots for the numerical features, and are indicated as circles outside the range calculated using the IQR rule or approach.
<img width="859" alt="Screen Shot 2022-06-17 at 12 41 05 PM" src="https://user-images.githubusercontent.com/42109704/174340860-f90f9f13-61d6-4805-9a86-9ab25f070623.png">

The figure shows that all columns, except the ‘total protein’, has outliers. We need to remove the outliers, as they could contain critical information, for the given dataset, as the cause of death could be some anomalous symptoms associated with colic. If present, can introduce bias and affect the prediction. Hence removed. Here we use the capping approach, and the upper and lower bounds of the IQR method () are used as capping levels, to indicate any information that could have been present in these extreme data points.

