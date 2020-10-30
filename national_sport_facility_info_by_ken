
# Web scarping for the store location info of National Sport Facility Data.
# 1st step: Use Google Chrome and connect to TW Carrefour store info site > press "F12" to launch developer mode > click "XHR" to identify the API link
# 2nd step: Use postman app to test API link and identify the parameters for gathering data
# 3rd step: Use below PYTHON code to scarp information form the website & run the code on Google Colaboratory.

----------------------------------------------------------------------------------------

import requests
import pandas as pd
import json 

# 建立一個city list

cities = ['臺北市','新北市', '基隆市', '桃園市', '新竹縣', '新竹市', 
        '苗栗縣', '臺中市', '彰化縣','南投縣', '雲林縣', '嘉義縣', '臺南市', '高雄市', '屏東縣', '臺東縣',
        '花蓮縣', '宜蘭縣', '金門縣'] 



box = []

for index, city in enumerate(cities):
  data = {'city' : city}
  res = requests.get(url = 'https://iplay.sa.gov.tw/api/GymSearchAllList', params = data)
  res = json.loads(res.text) 
  box.append(res)


facility_table = pd.DataFrame(columns = ['facility_id', 'facility_name', 'facility_address', 'facility_type'])

def loop():
  for info in facility_city:
    for k,v in info.items():
      if k == 'GymID':
        f_id = v
        #print(f_id)
      elif k == 'Name':
        f_name = v
        #print(f_name)
      elif k == 'Address':
        f_add = v
        #print(f_add)
      elif k == 'GymFuncList':
        f_type = v
        #print(f_type)
        new_row = {'facility_id' : f_id, 'facility_name' : f_name, 'facility_address' : f_add, 'facility_type' : f_type}
         #print(new_row)
        global facility_table
        facility_table = facility_table.append(new_row, ignore_index= True)

    

for i in range(len(box)):
    facility_city = box[i]
    loop()


facility_table.to_csv('全國運動中心資料.csv', encoding="UTF-8", index=False)

