# Wechat_Export
Export WeChat Msgs to make fun graphs.

# 1. Export Wechat Database
On mac, backup iPhone to the latest version and DON'T ENCRYPT. Then, using third part app to export wechat database. Eg: iPhone Backup Extractor. It only allows to export 4 files in one export. The file path in the backup is ```/Users/kelo/Documents/WeChat_Export/Applications/com.tencent.xin/Documents/YOURID/DB/MM.sqlite```

In case of you have logged several wechat accounts on your iPhone before, you can use a sqlite database to take a look at each MM.sqlite file first.

If you backed your wechat history on Wechat in mac, you can also export Wechat database in the following path ```/Users/YOURCOMPNAME/Library/Containers/com.tencent.xinWeChat/Data/Library/Application Support/com.tencent.xinWeChat/2.0b4.0.9/YOURID/Message'''
Wechat use sqlcipher to store its database, which is an open source tool. So, after we get raw-key for our databases, we can export it. To get the raw-key, first open Wechat, without logging, and type 
```
lldb -p $(pgrep WeChat)
br set -n sqlite3_key
c
```
Then log in Wechat, and type
```
memory read --size 1 --format x --count 32 $rsi
```
Then get a key like this:
```
0x60000363e160: 0x5e 0x92 0x31 0xa5 0x1d 0x0c 0x4c 0x25
0x60000363e168: 0x99 0x83 0x58 0xd2 0x55 0x73 0x9e 0x98
0x60000363e170: 0xe5 0xd7 0xfa 0x65 0x0b 0x3d 0x46 0x30
0x60000363e178: 0x83 0xf9 0x68 0xd5 0xda 0xe9 0x31 0xbc
```
In each line after colon, delete 0x and add all other characters, then add 0x at the start. For example: 
```
0x5e9231a51d0c4c25998358d255739e98e5d7fa650b3d463083f968d5dae931bc
```

Then download a sqlite browser, for example, https://links.jianshu.com/go?to=https%3A%2F%2Fsqlitebrowser.org%2F
Open a new database-change RAW-KEY from paraphrase-input Password-Select SQLCipher 3 defaults. Then you will be able to edit databases, or export csv to do analysis.

I would prefer to use the first method, as databases are stored into a couple of .db files throught the backup on mac in Wechat app.

Note, the information contained in this guide is for educational purposes only.
