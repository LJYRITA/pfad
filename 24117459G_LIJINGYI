import requests
from bs4 import BeautifulSoup

url = 'https://lishi.tianqi.com/beijing/202408.html'
headers = {'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/128.0.0.0 Safari/537.36'}
response = requests.get(url, headers=headers)

if response.ok:
    print('Data OK')
else:
    print(f'Response Status Code: {response.status_code}')

html = response.text
soup = BeautifulSoup(html, 'html.parser')
data=[]
datas=[]
all_th140s = soup.findAll('div', attrs={'class': "th140"})

for i in all_th140s:
    item=i.string
    data.append(item)
for i in data:
    i=i.replace('℃','')
    if i.isdigit():
        i=float(i)
        datas.append(i)

import matplotlib.pyplot as plt
import pandas as pd
import numpy as np

new_column_names = ['HighestTemp A', 'LowestTemp B']
df = pd.DataFrame(np.array(datas).reshape(10, 2), columns=new_column_names)
print(df)

plt.figure(figsize=(10, 6))
for i in range(df.shape[1]):
    plt.plot(df.index, df.iloc[:, i], label=df.columns[i])

plt.xlabel('date')
plt.ylabel('temperature')
plt.title('Beijing')
plt.legend(title='TempChange')
plt.show()
