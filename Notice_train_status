# Jap: 特定のルートの電車の運行状況を自分のLINEに通知するプログラム。
# Eng: The program it notice you the status of trains which you use.
# Use 'LINE' application.
import requests
from bs4 import BeautifulSoup
import time
import datetime

# date when you get the data
today = datetime.datetime.now().strftime('%Y/%m/%d %H:%M:%S')
# TOKEN you got
LINE_TOKEN = 'Your TOKEN'
# URL of API
api_url_line = 'https://notify-api.line.me/api/notify'

# message contents
send_contents = {'date': today}
print(send_contents)    # record to log

TOKEN_dic = {'Authorization': 'Bearer' + ' ' + LINE_TOKEN}
send_contents = {'message': today + 'の運行状況'}
requests.post(api_url_line, headers=TOKEN_dic, data=send_contents)

# 武蔵野線URL (Musashino-line)
musashi_url = 'https://transit.yahoo.co.jp/diainfo/71/0'
# 京浜東北線URL (Keihin Tohoku-line)
keihin_url = 'https://transit.yahoo.co.jp/diainfo/22/0'
# 宇都宮線URL (Utsunomiya-line)
utsunomiya_url = 'https://transit.yahoo.co.jp/diainfo/46/46'

url_list = [musashi_url, keihin_url, utsunomiya_url]
name_list = ['武蔵野線', '京浜東北線', '宇都宮線']

# function which gets informatino of trains status
def get_train_status(url, name):
    req = requests.get(url)
    time.sleep(2)
    soup = BeautifulSoup(req.text, 'html.parser')

    if soup.find('dd', class_='normal'):
        message = name + 'は通常運転です。'
    else:
        message = [soup.find(class_='trouble').text, url]
    
    send_dic = {'message': message}
    requests.post(api_url_line, headers=TOKEN_dic, data=send_dic)

# execute the function
for i in range(3):
    get_train_status(url_list[i], name_list[i])
    
print('finished!!') # record to log
