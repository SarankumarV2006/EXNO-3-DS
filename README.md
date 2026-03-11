## EXNO-3-DS

# AIM:
To read the given data and perform Feature Encoding and Transformation process and save the data to a file.

# ALGORITHM:
STEP 1:Read the given Data.
STEP 2:Clean the Data Set using Data Cleaning Process.
STEP 3:Apply Feature Encoding for the feature in the data set.
STEP 4:Apply Feature Transformation for the feature in the data set.
STEP 5:Save the data to the file.

# FEATURE ENCODING:
1. Ordinal Encoding
An ordinal encoding involves mapping each unique label to an integer value. This type of encoding is really only appropriate if there is a known relationship between the categories. This relationship does exist for some of the variables in our dataset, and ideally, this should be harnessed when preparing the data.
2. Label Encoding
Label encoding is a simple and straight forward approach. This converts each value in a categorical column into a numerical value. Each value in a categorical column is called Label.
3. Binary Encoding
Binary encoding converts a category into binary digits. Each binary digit creates one feature column. If there are n unique categories, then binary encoding results in the only log(base 2)ⁿ features.
4. One Hot Encoding
We use this categorical data encoding technique when the features are nominal(do not have any order). In one hot encoding, for each level of a categorical feature, we create a new variable. Each category is mapped with a binary variable containing either 0 or 1. Here, 0 represents the absence, and 1 represents the presence of that category.

# Methods Used for Data Transformation:
  # 1. FUNCTION TRANSFORMATION
• Log Transformation
• Reciprocal Transformation
• Square Root Transformation
• Square Transformation
  # 2. POWER TRANSFORMATION
• Boxcox method
• Yeojohnson method

# CODING AND OUTPUT:

```
import pandas as pd
import numpy as np
from scipy import stats
df = pd.read_csv('data.csv')
df
```
<img width="681" height="301" alt="image" src="https://github.com/user-attachments/assets/640f4b8c-ff72-4bd5-96bf-69999f3556ef" />

```
from sklearn.preprocessing import OrdinalEncoder,LabelEncoder
climate = ['Cold','Warm','Hot','Very Hot']
ele = OrdinalEncoder(categories=[climate])
ele.fit_transform(df[["Ord_1"]])
```
<img width="438" height="200" alt="image" src="https://github.com/user-attachments/assets/cb1893fa-be81-499c-b55e-df071019ff7d" />

```
df['bo2'] = ele.fit_transform(df[["Ord_1"]])
df
```
<img width="687" height="302" alt="image" src="https://github.com/user-attachments/assets/1dff432f-5677-4087-9a4f-cafd6cfdcfc9" />

```
le = LabelEncoder()
df2 = df.copy()
df2['Ord_2'] = le.fit_transform(df2['Ord_2'])
df2
```

<img width="745" height="304" alt="image" src="https://github.com/user-attachments/assets/f27f7803-8d8b-4834-be03-8ef4536c0daa" />

```
df2['Ord_2'] = le.fit_transform(df2['Ord_2'])
df2
```

<img width="782" height="300" alt="image" src="https://github.com/user-attachments/assets/10c01ed2-26f9-4a1d-a65d-88a316c8ab55" />

```
from sklearn.preprocessing import OneHotEncoder
ohe = OneHotEncoder()
df3 = df.copy()
enc = pd.DataFrame(ohe.fit_transform(df2[["City"]]))
df2 = pd.concat([enc,df3],axis = 1)
df2
```

<img width="876" height="295" alt="image" src="https://github.com/user-attachments/assets/832511c1-fb30-4299-97ad-e24c21f038d7" />

```
pd.get_dummies(df,columns=['City'])
```
<img width="885" height="297" alt="image" src="https://github.com/user-attachments/assets/095f9fc9-856b-4cfa-982f-4a0b48ee662c" />

```
from category_encoders import BinaryEncoder
df = pd.read_csv('data.csv')
df
```
<img width="500" height="303" alt="image" src="https://github.com/user-attachments/assets/9cf19b1c-5e28-4724-97b6-6f2c6fd21b2f" />

```
be = BinaryEncoder()
nd = be.fit_transform(df['Ord_2'])
df
```
<img width="503" height="290" alt="image" src="https://github.com/user-attachments/assets/1186c914-075e-468c-92b3-5f8ae15a8c7c" />

```
from cate
gory_encoders import TargetEncoder
te = TargetEncoder()
CC = df.copy()
new = te.fit_transform(CC["City"],y=CC["Target"])
CC = pd.concat([CC,new],axis = 1)
CC
```
<img width="582" height="289" alt="image" src="https://github.com/user-attachments/assets/2710807c-cb13-4698-bf13-993a1f6c06a0" />

```
if 'City' in CC.columns:
    CC = CC.drop('City', axis=1)
new = te.fit_transform(X = df["City"],y=df["Target"])
CC = pd.concat([CC.reset_index(drop=True),new.reset_index(drop=True)],axis = 1)
CC
```
<img width="506" height="295" alt="image" src="https://github.com/user-attachments/assets/ef9db174-57f6-4c74-b6d8-8447e4a01f50" />

```
df = pd.read_csv('Data_to_Transform.csv')
df
```
<img width="723" height="360" alt="image" src="https://github.com/user-attachments/assets/3162e10c-51b3-4f0d-bd68-3f0872d8ba51" />

```
df.skew()
```
<img width="296" height="179" alt="image" src="https://github.com/user-attachments/assets/7b9226cf-d918-4c4b-a0eb-bbd03b327de3" />

```
np.log(df["Highly Positive Skew"])
```
<img width="783" height="218" alt="image" src="https://github.com/user-attachments/assets/521f59d5-4034-4da7-ab16-0866855edca0" />

```
np.reciprocal(df["Moderate Positive Skew"])
```
<img width="663" height="232" alt="image" src="https://github.com/user-attachments/assets/7d177f0c-12db-4bf0-82ba-2a7bd6fc93ba" />

```
np.sqrt(df["Highly Positive Skew"])
```

<img width="668" height="244" alt="image" src="https://github.com/user-attachments/assets/c6ef7c71-dbd3-438f-8469-d225337d99dc" />

```
np.square(df["Highly Positive Skew"])
```

<img width="674" height="245" alt="image" src="https://github.com/user-attachments/assets/b198bf08-85d1-44ab-a039-f584e4b6f569" />

```
df["Highly Positive Skew_boxcox"], parameters = stats.boxcox(df["Highly Positive Skew"])
df
```

<img width="931" height="386" alt="image" src="https://github.com/user-attachments/assets/0b01dfd4-4589-491a-9ab9-9f840fab52da" />

```
df["Moderate Negative Skew_yeojohnson"], parameters = stats.yeojohnson(df["Moderate Negative Skew"])
df
```
<img width="903" height="398" alt="image" src="https://github.com/user-attachments/assets/91ac6efc-c383-42ea-b46e-59a6b47a98a9" />

```
from sklearn.preprocessing import QuantileTransformer
qt = QuantileTransformer(output_distribution = 'normal')
df["Moderate Negative Skew_1"] = qt.fit_transform(df[["Moderate Negative Skew"]])
df
```
<img width="882" height="382" alt="image" src="https://github.com/user-attachments/assets/c2be6766-8540-4ef7-8a6c-36f1ebc36738" />

```
import matplotlib.pyplot as plt
import seaborn as sns
import statsmodels.api as sm
import scipy.stats as stats
sm.qqplot(df["Moderate Negative Skew"],line = '45')
plt.show()
```

<img width="827" height="496" alt="image" src="https://github.com/user-attachments/assets/e9364d44-87ff-42d3-948c-1a70a40d0d86" />

```
sm.qqplot(df["Moderate Negative Skew_1"],line = '45')
plt.show()
```

<img width="958" height="487" alt="image" src="https://github.com/user-attachments/assets/fe8870db-50dc-401a-884c-034287bc9236" />

```
df["Highly Negative Skew_1"] = qt.fit_transform(df[["Highly Negative Skew"]])
sm.qqplot(df["Highly Negative Skew"],line = '45')
plt.show()
```

<img width="784" height="489" alt="image" src="https://github.com/user-attachments/assets/4b8c07d6-f122-4bad-a084-9f7158f741f5" />

```
sm.qqplot(np.reciprocal(df["Moderate Negative Skew_1"]),line = '45')
plt.show()
```

<img width="853" height="477" alt="image" src="https://github.com/user-attachments/assets/97cccb10-601b-4fbe-9c2c-946aa019b1dc" />

```
sm.qqplot(df["Highly Negative Skew_1"],line = '45')
plt.show()
```
<img width="852" height="485" alt="image" src="https://github.com/user-attachments/assets/b25a5f48-24d8-4002-8511-990388cecd41" />

```
sm.qqplot(np.abs(df["Highly Negative Skew_1"]),line = '45')
plt.show()
```

<img width="975" height="493" alt="image" src="https://github.com/user-attachments/assets/1a53ee54-688a-4b03-833c-5a0b66e214e0" />

```
sm.qqplot(np.log(df["Highly Negative Skew_1"]),line = '45')
plt.show()
```

<img width="882" height="493" alt="image" src="https://github.com/user-attachments/assets/2f2cd3c0-35fa-4c9b-9f76-4929acff85f3" />

```
pd.concat([CC,new],axis = 1)
```

<img width="573" height="314" alt="image" src="https://github.com/user-attachments/assets/2728bb77-817b-4eb7-bfb0-66f232aed096" />





# RESULT:
Thus, we have successfully performed Feature Encoding and Transformation process and saved the data to a file.



       
