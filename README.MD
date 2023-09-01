# Ubuntu 定時排程設定

## 查看排程列表

```bash
crontab -l
```

## 編輯排程列表

```bash
crontab -e
```

如果要指定編輯器 (習慣使用vim)
```bash
VISUAL=vim crontab -e
```

## 設定排程
進入編輯模式後，前往最後一行新增排程
### 格式範例
```text
 ┌───────────── 分鐘   (0 - 59)
 │ ┌─────────── 小時   (0 - 23)
 │ │ ┌───────── 日     (1 - 31)
 │ │ │ ┌─────── 月     (1 - 12)
 │ │ │ │ ┌───── 星期幾 (0 - 7，0 是週日，6 是週六，7 也是週日)
 │ │ │ │ │
 * * * * * /path/to/command
```

### 特殊字元
```text
星號(*): 代表接受任意時刻，例如若在月份那一欄填入星號，則代表任一月份皆可。
逗號(,): 分隔多個不同時間點。例如若要指定 3:00、6:00 與 9:00 三個時間點執行指令，就可以在第二欄填入 3,6,9。
減號(-): 代表一段時間區間，例如若在第二欄填入 8-12 就代表從 8 點到 12 點的意思，也就是等同於 8,9,10,11,12。
斜線加數字(/n): n 代表數字，這樣寫的意思就是「每隔 n 的單位」的意思，例如若在第一欄填入 */5 就代表每間隔五分鐘執行一次的意思，也可以寫成 0-59/5。
```

### 設定範例
```bash
# 每小時的第 30 分鐘執行一次python
30 * * * * /usr/bin/python3 /path/to/your/python/script.py

# 每天早上 8 點 30 分執行
30 08 * * * /home/gtwang/script.sh --your --parameter

# 每週日下午 6 點 30 分執行
30 18 * * 0 /home/gtwang/script.sh --your --parameter

# 每週日下午 6 點 30 分執行
30 18 * * Sun /home/gtwang/script.sh --your --parameter

# 每年 6 月 10 日早上 8 點 30 分執行
30 08 10 06 * /home/gtwang/script.sh --your --parameter

# 每月 1 日、15 日、29 日晚上 9 點 30 分各執行一次
30 21 1,15,29 * * /home/gtwang/script.sh --your --parameter

# 每隔 10 分鐘執行一次
*/10 * * * * /home/gtwang/script.sh --your --parameter

# 從早上 9 點到下午 6 點，凡遇到整點就執行
00 09-18 * * * /home/gtwang/script.sh --your --parameter
```

## docker crontab設置

[link](https://github.com/adiii717/docker-python-cronjob)