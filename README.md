# 🎯 A/B Testing for Subscription Banner – Ecommerce Case Study

<img width="1200" height="628" alt="image" src="https://github.com/user-attachments/assets/afabc36e-cba5-4fb2-bdd6-e01101c0b8df" />

## 📌 **Project Overview**

This project explores an A/B testing experiment conducted for an eCommerce business that offers a special membership subscription promotion to a selected group of users (whitelist customers).

Originally, customers were shown a promotional banner (referred to as Screen A) that displayed the discounted subscription price of 99K VND (from the original 199K VND). However, the conversion rate — i.e., the percentage of users who purchased the subscription — was lower than expected.

To improve performance, the business proposed a new version of the banner (Screen B) which instead emphasized the discount amount ("Save 100K") rather than showing the final price directly.

## 🧪 **A/B Testing Design**

This project includes a well-defined A/B test experiment to evaluate which banner performs better in terms of driving user conversion.

🔍 **Key Components:**

1. Hypothesis:

    - Null Hypothesis (H₀): There is no significant difference in conversion rate between Screen A and Screen B.

    - Alternative Hypothesis (H₁): There is a significant difference in conversion rate between the two screens.

2. Metric Tracked:

    - Conversion Rate = Number of users who purchased / Total number of users in each group

3. Sample Pool:

    - Only whitelist customers (eligible for the promotion)

    - Randomly divided into:

      - Group 1: View Screen A (shows price 99K)

      - Group 2: View Screen B (shows “Discount 100K”)

4. Confounding Control:

- Users were randomly assigned to groups to avoid selection bias

- Other factors like time of exposure, user location, and app performance were assumed constant for the test

5. External Factors to Consider:

- Time of day/week the banners were shown

- Ongoing campaigns

- Device differences (mobile vs desktop)

- Technical issues affecting banner visibility

## 📊 Dataset Description

The dataset used in this experiment contains anonymized user behavior and group assignment. It includes:

| Column | Description |
| - | - |
| customer_id | Unique ID of each user |
| group |	1 = Screen A, 2 = Screen B |
| is_buy |	1 if the user purchased, 0 otherwise |

## 🛠️ Tools & Environment

- Python (Pandas, Seaborn, Statsmodels)

- Google Colab for code and visualization

- abtestguide.com for z-test validation

## 📈 Analysis & Results

[**Link to code**](https://colab.research.google.com/drive/1cagj1xEml9PNc9EdBZEm_QJahm4tmRnu?usp=sharing)

### ✅ Hypothesis

* Null Hypothesis (H₀): There is no difference in conversion rate between users who see Screen A and Screen B.

* Alternative Hypothesis (H₁): There is a significant difference in conversion rate between Screen A and Screen B.

### ✅ Import libraries

```ruby
!pip install pydantic-settings
!pip install pandas==2.1.4 ydata-profiling==4.6.4

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
import datetime as dt
import plotly.express as px
import scipy.stats as ss
import math as mt
import itertools

from wordcloud import WordCloud
from ydata_profiling import ProfileReport
```

### ✅ EDA (Exploratory Data Analysis)

```ruby
import os
os.chdir('/content/drive/MyDrive/DAC 1 on 1 /ML/K35_Pham Thanh Tung_Project 1')
df_abtest = pd.read_csv('abtesting.csv')
df_abtest.head()
```

<img width="1088" height="379" alt="image" src="https://github.com/user-attachments/assets/771c6be4-3a0c-442a-bab4-1f90654907c7" />

<img width="1088" height="310" alt="image" src="https://github.com/user-attachments/assets/75751c5a-5d0e-4232-9ef6-7f52b68fbeeb" />

<img width="1088" height="432" alt="image" src="https://github.com/user-attachments/assets/5491a4d8-c6bc-41c7-8bb7-2ae0d8dfa715" />

<img width="1088" height="523" alt="image" src="https://github.com/user-attachments/assets/26e1d9cf-5ec2-45b8-8c6f-38ddbbb85b95" />

<img width="1088" height="308" alt="image" src="https://github.com/user-attachments/assets/6cc0e452-05ab-4f88-82e5-dc1ea523a191" />

### ✅ Visualize conversion rates

```ruby
summary_plot = summary.reset_index()
sns.barplot(x='group', y='conversion_rate', data=summary_plot)
plt.title("Conversion Rate by Group")
plt.ylabel("Conversion Rate")
plt.xlabel("Group")
plt.ylim(0, summary['conversion_rate'].max() + 0.05)
plt.show()
```

<img width="1088" height="573" alt="image" src="https://github.com/user-attachments/assets/54f9d113-d825-4a70-be22-2f9cc78ce1bd" />

### ✅ Hypothesis Testing (Two-proportion z-test)

```ruby
from statsmodels.stats.proportion import proportions_ztest

# Extract conversion counts and sample sizes
successes = summary['sum'].tolist()         # number of buyers
samples = summary['count'].tolist()         # total users in group

z_stat, p_val = proportions_ztest(count=successes, nobs=samples)

print(f"\nZ-statistic: {z_stat:.4f}")
print(f"P-value: {p_val:.4f}")
```

<img width="1088" height="98" alt="image" src="https://github.com/user-attachments/assets/a04aee70-77a2-4d46-a274-e4c6606484a8" />

### ✅ Interpret result

<img width="1088" height="234" alt="image" src="https://github.com/user-attachments/assets/7ea8d784-9cba-4c8b-8d75-af0a36ac7e42" />

### ✅ Conclusion and Recommendation

After analyzing the results:

* The conversion rate for Screen B was significantly higher than for Screen A

* A two-proportion z-test confirmed that this difference is statistically significant (p < 0.05), indicating that the observed effect is unlikely due to chance.

🔍 **Interpretation:**

Customers responded better to the message that emphasized the discount amount (e.g. "-100K") rather than the final price. This aligns with behavioral insights that suggest users perceive higher value when the savings are made explicit.

📌 **Recommendation:**

Based on the statistical evidence and improved conversion rate, we recommend releasing Screen B (showing "-100K" discount) to all eligible users, as it drives higher conversion and has been validated through a statistically sound A/B test.


