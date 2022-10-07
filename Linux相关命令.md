##### 1. 切换为root

```bash
su -
```

切换为原用户

```
exit
```

##### 2. 切换tty

命令行登陆：

```
[Ctrl] + [Alt] + [F2~F6]
```

图形接口桌面：

```
[Ctrl] + [Alt] + [F1]
```

命令行启动图形界面：

```
startx
```

##### 3. 显示日期时间

```
date +%Y/%m/%d
date +%H:%M
```

##### 4. 显示日历

```
cal
cal [year]
cal [month] [year]
```

##### 5. 计算机：bc

```
bc #进入计算机
scale=[number] #设置小数点位
quit #退出bc
```

##### 6. [Tab]键

- 接在第一个输入的数据后面为命令补全；
- 接在第二个输入的数据后面为文件不齐；
- 接在某些指令后面又选项/参数补齐的功能；

##### 7. [Ctrl] + c

- 停止正在运行的程序；

##### 8. [Ctrl] + d

- 离开命令行（相当于exit）；

##### 9. 前后翻页

```
[shift] + [PageUP]/[Page Down]
```

##### 10. 指令帮助

```
[command] --help
man [command]
info [command]
```

##### 11. nano文书编辑器

```
nano text.txt #存在就打开旧文件，不存在就打开新文件
```

- [Ctrl] + G：取得线上说明；
- [Ctrl] + X：离开nano；
- [Ctrl] + O：存储盘案；
- [Ctrl] + R：从其他文件读入数据；
- [Ctrl] + W：搜寻字符；
- [Ctrl] + C：说明目前光标所处的行数与列数；
- [Ctrl] + 行号：快速移动到该行；
- [alt] + Y：校正语法功能打开或关闭；
- [alt] + M：支持鼠标来移动光标；

##### 12. 关机

```
sync #将数据同步写入硬盘
shutdown -h now #立刻关机
shutdown -h [time] #指定时间关机
shutdown -h +10 #10min后关机
shutdown -r now #立刻重启
shutdown -r +10 ‘notice’ #10min后重启并将notice发送给所有线上使用者
shutdown -k now ‘notice’ #仅发出警告信息不会关机
systemctl halt #系统停止
systemctl poweroff #系统直接关机
systemctl reboot #直接重新开机
systemctl suspend #进入休眠模式
```





