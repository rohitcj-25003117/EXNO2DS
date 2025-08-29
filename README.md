# EXNO2DS
# AIM:
      To perform Exploratory Data Analysis on the given data set.
      
# EXPLANATION:
  The primary aim with exploratory analysis is to examine the data for distribution, outliers and anomalies to direct specific testing of your hypothesis.
  
# ALGORITHM:
STEP 1: Import the required packages to perform Data Cleansing,Removing Outliers and Exploratory Data Analysis.

STEP 2: Replace the null value using any one of the method from mode,median and mean based on the dataset available.

STEP 3: Use boxplot method to analyze the outliers of the given dataset.

STEP 4: Remove the outliers using Inter Quantile Range method.

STEP 5: Use Countplot method to analyze in a graphical method for categorical data.

STEP 6: Use displot method to represent the univariate distribution of data.

STEP 7: Use cross tabulation method to quantitatively analyze the relationship between multiple variables.

STEP 8: Use heatmap method of representation to show relationships between two variables, one plotted on each axis.

## CODING AND OUTPUT

        import pandas as pd
        import seaborn as sns

        df=pd.read_csv("titanic_dataset.csv")
        df
<img width="1055" height="417" alt="image" src="https://github.com/user-attachments/assets/3c1485cb-5c24-4f4a-a1b0-534423587030" />

        df.shape
        df.info()
        df.describe()
        
<img width="416" height="422" alt="image" src="https://github.com/user-attachments/assets/88918e72-58bb-4c26-863d-cf0e990e9327" />

<img width="816" height="362" alt="image" src="https://github.com/user-attachments/assets/492badd4-5399-46ed-ac56-76de01a293ba" />

        df.set_index("PassengerId",inplace=True)
        df
<img width="1070" height="437" alt="image" src="https://github.com/user-attachments/assets/cab202ba-48b4-4cbe-9606-2bd819f49b36" />

        df.isnull()
<img width="768" height="507" alt="image" src="https://github.com/user-attachments/assets/80270149-bff6-458a-b605-3e1e220d8592" />

        print(df.isnull().sum())
        df.nunique()
        
<img width="207" height="333" alt="image" src="https://github.com/user-attachments/assets/746a587a-5543-4e93-aee3-77a53ad80b8c" />

        #total values
        df['Survived'].value_counts()
        
<img width="976" height="135" alt="image" src="https://github.com/user-attachments/assets/bd7dcf0e-e742-40b3-99c9-b3716930f0c8" />

        #unique values in that column
        df.Survived.unique()
        
<img width="192" height="57" alt="image" src="https://github.com/user-attachments/assets/97c29499-4e4a-4a1d-b86e-5b2d8ceb8fb1" />

        #univariate analysis
        #grouping based on sex
        sns.countplot(x="Survived",hue='Sex',data=df)
        
<img width="622" height="466" alt="image" src="https://github.com/user-attachments/assets/b775c567-86f2-48c3-a2b6-1e802b7c59d6" />

        df.rename(columns={'Sex':'Gender'},inplace=True)
        df
        
<img width="1019" height="420" alt="image" src="https://github.com/user-attachments/assets/ddf1cb2e-c6ff-43c0-b28f-7d9b4afbe3dd" />

        sns.countplot(x="Gender",hue='Pclass',data=df)
        
<img width="721" height="528" alt="image" src="https://github.com/user-attachments/assets/7a14a8ff-3ac2-4ef5-9d3e-30d83302132c" />

        sns.catplot(x="Survived",hue="Gender",data=df,kind='violin')
        
<img width="867" height="697" alt="image" src="https://github.com/user-attachments/assets/d71de545-5f86-4fb8-a4c0-78c076b0e5a8" />

        sns.catplot(x="Survived",hue="Gender",data=df,kind='count')

<img width="898" height="717" alt="image" src="https://github.com/user-attachments/assets/5a8eab9c-de02-4040-9556-a8ca88ed629a" />

        sns.catplot(x="Survived",col="Gender",data=df,kind='count')

<img width="997" height="518" alt="image" src="https://github.com/user-attachments/assets/7c2c5587-5a62-4c2a-ac65-b5842941543a" />

        sns.boxplot(data=df)

<img width="833" height="626" alt="image" src="https://github.com/user-attachments/assets/00d984c2-340c-4f6f-918f-93484b7048c5" />

        df.boxplot(column='Age',by='Pclass')
        
<img width="721" height="567" alt="image" src="https://github.com/user-attachments/assets/aedcfc37-bc0a-4218-8e17-f42a88c16c60" />

        sns.scatterplot(x='Age',y='Fare',data=df)

<img width="728" height="562" alt="image" src="https://github.com/user-attachments/assets/2d3e2268-ef5a-4eaf-be27-8aeb79be2eb5" />

        sns.jointplot(x='Age',y='Fare',data=df)

<img width="717" height="696" alt="image" src="https://github.com/user-attachments/assets/0b04542d-7181-42bc-93e2-3257cbedb9f4" />

        sns.jointplot(x='Age',y='Fare',data=df,kind='kde')

<img width="832" height="853" alt="image" src="https://github.com/user-attachments/assets/23174e43-4b1e-4496-9c4b-4489651a83b8" />

        sns.jointplot(x='Age',y='Fare',data=df,kind='hist')

<img width="762" height="761" alt="image" src="https://github.com/user-attachments/assets/d4741b1f-0fb8-49b1-9b83-5228c08f7773" />

          #pairwise relationship
        sns.pairplot(data=df)
        
<img width="1053" height="620" alt="image" src="https://github.com/user-attachments/assets/a65f2a8d-afd3-479d-91cc-bcafc4df9efb" />

        #multivariate analysis
        cor1=df.select_dtypes(include=['number']).corr()
        sns.heatmap(cor1,annot=True)
        
<img width="873" height="713" alt="image" src="https://github.com/user-attachments/assets/8edeba23-355b-4172-9d47-59173ca51c54" />

                group=df.groupby(['Pclass','Survived'])
        pclass_survived=group.size().unstack()
        sns.heatmap(pclass_survived,annot=True,fmt='d')

<img width="856" height="655" alt="image" src="https://github.com/user-attachments/assets/552c3fd7-6507-4db3-afb0-c5f28069b472" />

        
 
























# RESULT
            Thus the given titanic dataset is analysed through exploratory data analysis.
