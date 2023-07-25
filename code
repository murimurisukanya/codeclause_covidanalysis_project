# This Python 3 environment comes with many helpful analytics libraries installed
# It is defined by the kaggle/python Docker image: https://github.com/kaggle/docker-python
# For example, here's several helpful packages to load

import numpy as np # linear algebra
import pandas as pd # data processing, CSV file I/O (e.g. pd.read_csv)

# Input data files are available in the read-only "../input/" directory
# For example, running this (by clicking run or pressing Shift+Enter) will list all files under the input directory

import os
for dirname, _, filenames in os.walk('/kaggle/input'):
    for filename in filenames:
        print(os.path.join(dirname, filename))

# You can write up to 20GB to the current directory (/kaggle/working/) that gets preserved as output when you create a version using "Save & Run All" 
# You can also write temporary files to /kaggle/temp/, but they won't be saved outside of the current session
          import matplotlib.pyplot as plt
import seaborn as sns
import plotly.express as px
from plotly.subplots import make_subplots
import datetime
covid_df=pd.read_csv("../input/covid-19-india/covid_19_india.csv")
  covid_df.head(10)
  covid_df.info()
  covid_df.describe()
  vaccine_df=pd.read_csv("../input/covid-19-india/covid_vaccine_statewise.csv")
  vaccine_df.head(10)
  vaccine_df.info()
  vaccine_df.describe()
  covid_df.drop(["Sno","Time","ConfirmedIndianNational","ConfirmedForeignNational"],inplace=True,axis=1)
  covid_df.head()
  covid_df['Date']=pd.to_datetime(covid_df['Date'],format='%Y-%m-%d')
covid_df.head()
covid_df.info()
covid_df['Active_cases']=covid_df['Confirmed']-(covid_df['Cured']+covid_df['Deaths'])
covid_df.tail()
covid_df['State/UnionTerritory']=covid_df['State/UnionTerritory'].replace('Maharashtra***',"Maharashtra")
covid_df['State/UnionTerritory']=covid_df['State/UnionTerritory'].replace('Bihar****',"Bihar")
covid_df['State/UnionTerritory']=covid_df['State/UnionTerritory'].replace('Madhya Pradesh***',"Madhya Pradesh")
covid_df['State/UnionTerritory']=covid_df['State/UnionTerritory'].replace('Karanataka',"Karnataka")
#pivot table
statewise_data=pd.pivot_table(covid_df, values=['Confirmed','Deaths','Cured'],index="State/UnionTerritory", aggfunc=max)
statewise_data['Recovery Rate']=statewise_data['Cured']*100/statewise_data['Confirmed']
statewise_data=statewise_data.sort_values(by="Confirmed",ascending=False)
statewise_data.style.background_gradient(cmap="CMRmap")
top10ActiveCases=covid_df.groupby(by='State/UnionTerritory').max()[['Active_cases','Date']].sort_values(by=['Active_cases'],ascending=False).reset_index()
fig=plt.figure(figsize=(16,10))
plt.title("Top 10 states with most Active Cases  in India",size=22)
ax=sns.barplot(data=top10ActiveCases.iloc[:10],y='Active_cases',x='State/UnionTerritory',linewidth=2,edgecolor='black')
plt.xlabel("States")
plt.ylabel("Total Active Cases")
plt.show()
  top10Deaths=covid_df.groupby(by='State/UnionTerritory').max()[['Deaths','Date']].sort_values(by=['Deaths'],ascending=False).reset_index()
  fig=plt.figure(figsize=(16,10))
plt.title("Top 10 states with most Deaths in India",size=22)
ax=sns.barplot(data=top10Deaths.iloc[:10],y='Deaths',x='State/UnionTerritory',linewidth=2,edgecolor='black')
plt.xlabel("States")
plt.ylabel("Total Deaths")
plt.show()
  #Growth Trend
fig=plt.figure(figsize=(12,6))
ax=sns.lineplot(data=covid_df[covid_df['State/UnionTerritory'].isin(['Maharashtra','Karnataka','Kerala','Tamil Nadu','Uttar Pradesh'])],x='Date',y='Active_cases',hue='State/UnionTerritory')
#ax.set_title("Top 5 Affected States in India",size=16)
  vaccine_df.rename(columns={'Updated On':'Vaccine_Date'},inplace=True)
  vaccine_df.head()
  vaccine_df.isnull().sum()
  vaccination=vaccine_df.drop(columns=['Sputnik V (Doses Administered)','AEFI','18-44 Years (Doses Administered)','45-60 Years (Doses Administered)','60+ Years (Doses Administered)'],axis=1)
vaccination.head()
  male=vaccination['Male(Individuals Vaccinated)'].sum()
female=vaccination['Female(Individuals Vaccinated)'].sum()
px.pie(names=["Male","Female"],values=[male,female],title="Male vs Female Vaccination")
  vaccine=vaccine_df[vaccine_df.State!='India']
vaccine.head()
  vaccine.rename(columns={'Total Individuals Vaccinated':"Total"},inplace=True)
vaccine.head()
  #Most vaccinated State
max_vacc=vaccine.groupby('State')['Total'].sum().to_frame('Total')
max_vacc=max_vacc.sort_values(by='Total',ascending=False)[:5]
  fig=plt.figure(figsize=(12,5))
plt.title("Top 5 Vaccinated States in India",size=16)
x=sns.barplot(data=max_vacc.iloc[:10],y=max_vacc.Total,x=max_vacc.index,linewidth=2,edgecolor='black')
  #Least vaccinated State
min_vacc=vaccine.groupby('State')['Total'].sum().to_frame('Total')
min_vacc=min_vacc.sort_values(by='Total',ascending=True)[:5]
  fig=plt.figure(figsize=(12,5))
plt.title("Least 5 Vaccinated States in India",size=16)
x=sns.barplot(data=max_vacc.iloc[:10],y=min_vacc.Total,x=min_vacc.index,linewidth=2,edgecolor='black')
