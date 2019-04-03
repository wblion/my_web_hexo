---
title: 【持续更新原创】魔镜魔镜告诉我谁是世界上最美的人 树莓派diy魔镜第二弹 使用百度语音交互
date: 2018-10-29 11:52:46
tags:
---





大家好。借上次，我们系统安装完成之后，下面进入，与魔镜的交互部分，交互我们使用的是，百度的语音，和图灵的api。

先上视频  http://www.365yg.com/a6615223815368606222/#mid=51880178041

# 准备

因为我是使用的是百度和图灵，首先需要在这两个网站上面 申请账号，并得到key。

百度ai账号 

图灵 账号

# 步骤

#### 申请账号：

登录百度ai平台申请账号：

http://ai.baidu.com/



![](\img\mojingjiaohuo\baiduai.png)



创建应用语音合成语音识别记住你的id 和key

![](\img\mojingjiaohuo\baiduyingyong.png)

![](\img\mojingjiaohuo\key.png)

登录图灵申请账号

http://www.tuling123.com/

![](\img\mojingjiaohuo\tuling.png)

建立机器人 记录key

![](\img\mojingjiaohuo\creatrobot.png)





#### 安装库：

之后我后台连接树莓派给树莓派安装需要的库

```
pip install baidu-aip 安装百度语音的包
```

```
sudo apt-get install mpg123  用来播放mp3的音频

```

```
install  requests   提交图灵api的时候用的上
```

```
sudo apt-get install samba  
sudo apt-get install samba samba-common-bin 搭建samba服务 很有用，用来和台式机交互文件
```



#### 思路

![](\img\mojingjiaohuo\flow.png)





#### 代码（完整代码会在项目完成时候整理放到git上）

```
import os
import time
import requests
from json import loads
import json
from aip import AipSpeech
import time
import contextlib
import random

audio=Config.Config.audio
listen_voice_path=Config.Config.listen_voice_path
ll_voice_paths=Config.Config.all_return_voice



def speak_word(word_text):#说
    cover2mps(word_text)#转换音频
    play_mp3(audio)#播放音频

def cover2mps(word_text):# 这是使用百度的语音合成代码，来合成下面填入 APP_ID 和 API_KEY SECRET_KEY
    APP_ID = Config.Config.APP_ID
    API_KEY = Config.Config.API_KEY
    SECRET_KEY = Config.Config.SECRET_KEY

    client = AipSpeech(APP_ID, API_KEY, SECRET_KEY)

    result  = client.synthesis(word_text, 'zh', 1, {
        'vol': 5,"per":4,
    })
    if not isinstance(result, dict):
        with open(audio, 'wb') as f:
            f.write(result)


def play_mp3(filename):#使用 mpg123 播放MP3
    os.system('mpg123 %s' % (filename))

def think(text):#连接图灵api调用聊天模块
    #session=requests.session()
    url = 'http://openapi.tuling123.com/openapi/api/v2'
    data = {
        "reqType": 0,
        "perception": {
            "inputText": {
                "text": text
            },
            "selfInfo": {
                "location": {
                    "city": "",
                    "province": "",
                    "street": ""
                }
            }
        },
        "userInfo": {
            "apiKey": Config.Config.TU_LING_KEY,
            "userId": "123456lll"
        }
    }
    response = requests.post(url=url, data=json.dumps(data)).json()
    final_result=think_to_text(response)
    return  final_result


def think_to_text(return_result):
    for i in return_result["results"]:
        if i["resultType"] == "text":
            word_text = i["values"]["text"]
            print word_text
            return word_text

def get_file_content(filePath):
    with open(filePath, 'rb') as fp:
        return fp.read()


def voice_to_text(filePath):# 使用百度api吧声音传成文字
    APP_ID = Config.Config.APP_ID
    API_KEY = Config.Config.API_KEY
    SECRET_KEY = Config.Config.SECRET_KEY

    client = AipSpeech(APP_ID, API_KEY, SECRET_KEY)

    result  = client.asr(get_file_content(filePath), 'wav', 16000, {'dev_pid': 1536,})
    print result["err_msg"]
    if "success" in result["err_msg"]:
        return result["result"][0]
def go_listen():#听
    listen_voice_path = Config.Config.listen_voice_path
    os.system('arecord -f S16_LE -d 3 -r 16000 %s' % (listen_voice_path))


go_listen()#听 
works=voice_to_text(listen_voice_path）#声音转换为 文字
final_result = think(works)#文字传给图灵 进行想
speak_word(final_result)#说，想时候使用百度的语音合成返回，完成一次交互



```





待续搞起。。。。现在已经加入了语音唤醒，等我整理一下。希望更多的朋友关注支持，转载请注明出处。

共享交流群 14580005 一起用脑洞改变世界。相互研究帮助。 这是为了保证群成员质量和活性。需要收费3元请大家理解。







