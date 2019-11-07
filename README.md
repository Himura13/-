# -auto_get_filesctime
利用python批量获取文件的最早和最晚创建时间


import os
import time
import pandas as pd


base_dir = path# 根目录
filelist = os.listdir(base_dir)# 遍历路径下所有文件
time_2 = []

for a in range(0,len(filelist)):
    filename = filelist[a]
    act_filename = os.path.join(base_dir,filename)
    time_1 = os.path.getmtime(act_filename)
    time_2.append(time_1)
    time_3 = int(min(time_2))
    time_4 = int(max(time_2))
    start_time = time.strftime('%Y-%m-%d %H:%M',time.localtime(time_3))
    end_time = time.strftime('%Y-%m-%d %H:%M',time.localtime(time_4))
    
dataframe = pd.DataFrame({'start_time': start_time, 'end_time': end_time}, index=[0])
dataframe.to_csv("test.csv", index=False, sep=',')
