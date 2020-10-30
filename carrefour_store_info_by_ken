# Web scarping for the store location info of Taiwan Carrefour.
# 1st step: Use Google Chrome and connect to TW Carrefour store info site > press "F12" to launch developer mode > click "XHR" to identify the API link
https://docs.google.com/document/d/1d4fmOA7S1wOpbw72dwC8W71_I3SqyHc74Ka2dM_zZSk/edit
# 2nd step: Use postman app to test API link and identify the parameters for gathering data
# 3rd step: Use below PYTHON code to scarp information form the website.


----------------------------------------------------------------------------------------

import requests
import pandas as pd

# 建立一個區域的list

city = ['1','2', '3', '4', '5', '6', '7', '8'] 

# 1: 新北市
# 2: 台北市
# 3: 桃竹苗
# 4: 中彰投
# 5: 雲嘉南
# 6: 高屏
# 7: 宜花東
# 8: 金馬


#使用迴圈來依序取得每一個區域城市的門市資訊
box = []

#剛剛在開發者模式觀察到的get發出的資訊是那些

for index, city in enumerate(city):
  data = {
        'store_area_id':city,
        'is24h':'',
        'page_size':'all'
          }
  #print(data)
  res = requests.get(url = 'https://www.carrefour.com.tw/console/api/v1/stores', params=data)
  box.append(res.text)


store_table = pd.DataFrame(columns = ['store_name', 'store_address', 'store_type_name'])

def loop():
  for info in store_info:
    for k, v in info.items():
      if k == 'name':
         name = v
      # print(name)
      elif k== 'store_type_name':
         store_type = v
         #print(store_type)
      elif k == 'address':
         address = v
         #print(name)
         #print(store_type)
         #print(address)
         new_row = {'store_name' : name, 'store_type_name' : store_type, 'store_address' : address}
         #print(new_row)
         global store_table
         store_table = store_table.append(new_row, ignore_index= True)

    

#store_table = pd.DataFrame(columns = ['store_name', 'store_address', 'store_type_name'])

for i in range(len(box)):
  df_carrefour = pd.read_json(box[i])
  store_info =  df_carrefour.data.iloc[2]  
  loop()

store_table.to_csv('家樂福門市.csv', encoding="UTF-8", index=False)

