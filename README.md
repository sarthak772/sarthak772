import pandas as pd 
import requests


url = 'https://en.wikipedia.org/wiki/Template:COVID-19_pandemic_data'
req = requests.get(url)
data_list = pd.read_html(req.text)
target_df = data_list[0]

target_df.columns = ['Col0','country name','Total Cases','Total Deaths','Total Recoveries','Col5']
target_df = target_df[['country name','Total Cases','Total Deaths','Total Recoveries']]
target_df = target_df.drop([238,239])
target_df['country name'] = target_df['country name'].str.replace('\[.*\]','')
target_df['Total Recoveries'] = target_df['Total Recoveries'].str.replace('No data','0')
target_df.to_excel(r'covid19_dataset.xlsx ')
