# create telegram bot
1. 
# 用Python对接telegram机器人 处理command指令

import telebot
import time
import re
import youtube_dl
from dotenv import load_dotenv
import os

# 使用.env文件读取token
load_dotenv()
token = os.getenv('TOKEN')
