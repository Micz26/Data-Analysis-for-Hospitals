import pandas as pd
import matplotlib.pyplot as plt
pd.set_option('display.max_columns', 8)

general = pd.read_csv('test/general.csv')
prenatal = pd.read_csv('test/prenatal.csv')
sports = pd.read_csv('test/sports.csv')


# write your code here
prenatal = prenatal.rename(columns={'Sex': 'gender', "HOSPITAL": "hospital"})
sports = sports.rename(columns={"Male/female":'gender', "Hospital": "hospital"})
general1 = pd.concat([general, prenatal, sports], ignore_index=True)
general1 = general1.drop('Unnamed: 0', axis = 1)

general1 = general1.dropna(how='all')
replace_dict = {'man': 'm', 'male': 'm', 'woman' : 'f', 'female': 'f'}
general1["gender"] = general1["gender"].replace(replace_dict)
general1.loc[general1['hospital'] == 'prenatal', 'gender'] = general1.loc[general1['hospital'] == 'prenatal', 'gender'].fillna('f')
fill_dict = ['bmi', 'diagnosis', 'blood_test', 'ecg', 'ultrasound', 'mri', 'xray', 'children', 'months']
general1[fill_dict] = general1[fill_dict].fillna('0')
"""
first = general1['hospital'].value_counts().idxmax()
ratio = len(general1.loc[(general1['hospital'] == 'general') & (general1['diagnosis'] == 'stomach')]) / len(general1.loc[(general1['hospital'] == 'general')])
second = round(ratio, 3)
ratio2 = len(general1.loc[(general1['hospital'] == 'sports') & (general1['diagnosis'] == 'dislocation')]) / len(general1.loc[(general1['hospital'] == 'sports')])
third = round(ratio2, 3)
gen_df = general1[general1['hospital'].isin(['general'])]
spo_df = general1[general1['hospital'].isin(['sports'])]
fourth = gen_df['age'].median() - spo_df['age'].median()
T_blood = general1[general1["blood_test"] == 't']
fifth_df = T_blood.pivot_table(index='hospital', columns='blood_test', aggfunc='count')
fifth = fifth_df.idxmax()[0]
fifth2 = fifth_df.loc[fifth][0]
print(f'The answer to the 1st question is {first}')
print(f'The answer to the 2nd question is {second}')
print(f'The answer to the 3rd question is {third}')
print(f'The answer to the 4th question is {fourth}')
print(f'The answer to the 5th question is {fifth}, {fifth2} blood tests')
"""
age_list = []
bins = [0, 15, 35, 55, 70, 80]
for x in general1['age']:
    age_list.append(x)
plt.hist(age_list, bins =bins)
print("The answer to the 1st question: 15-35")
diagnosis = []
diagnosis_counts = []
for x in general1['diagnosis']:
    if x not in diagnosis:
        diagnosis.append(x)
        diagnosis_counts.append(0)
    diagnosis_counts[diagnosis.index(x)] += 1
plt.figure(figsize=(8,8))
plt.gca().set_aspect('equal')
plt.pie(diagnosis_counts, labels=diagnosis)
print("The answer to the 2nd question: pregnancy")
general_height = general1.loc[general1['hospital'] == 'general', 'height'].tolist()
prenatal_height = general1.loc[general1['hospital'] == 'prenatal', 'height'].tolist()
sports_height = general1.loc[general1['hospital'] == 'sports', 'height'].tolist()
data_list = [general_height, prenatal_height, sports_height]
fig, axes = plt.subplots()
plt.violinplot(data_list)
axes.set_ylabel("Height in meters")
axes.set_title('Height violin plot')
plt.show()
print("The answer to the 3rd question: It's because most patients are children or adults, so we see 2 peaks")
