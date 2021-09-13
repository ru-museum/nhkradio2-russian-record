# nhkradio2-russian-record
NHKラジオ第２ ロシア語番組録音

- これはNHKラジオ第２放送の「 ロシア語のラジオ番組」を**自動録音**するものです。
   - [ロシア語の番組案内](https://www2.nhk.or.jp/gogaku/russian/)  
   - [まいにちロシア語（入門編）](https://www.nhk.or.jp/radio/ondemand/detail.html?p=0956_01)  
   - [まいにちロシア語（応用編）](https://www.nhk.or.jp/radio/ondemand/detail.html?p=4414_01)

### NHKラジオ第2 番組表
 <table>
   <tr><th colspan="2" align="left">まいにちロシア語 入門編</th></tr>
   <tr><td>放　送</td><td>月～水曜日　午前8:50～9:05</td></tr>
  <tr><td>再放送</td><td>同日 月～水曜日　午後4:30～4:45</td></tr>
  <tr><td>再放送</td><td>翌週 月～水曜日　午後3:30～3:45</td></tr>
  <tr><th colspan="2" align="left">まいにちロシア語 応用編</th></tr>
  <tr><td>放　送</td><td>木・金曜日　午前8:50～9:05</td></tr>
  <tr><td>再放送</td><td>同日 木・金曜日　午後4:30～4:45</td></tr>
  <tr><td>再放送</td><td>翌週 木・金曜日　午後3:30～3:45</td></tr>
 </table>

# 動作環境  
- Linux(Debian: bash 使用)
- ffmpeg のインストールが必要です。

# 録音方法  
1. 作業フォルダに nhkradio2-russian-record.sh を置き編集します。  

　録音時間（必要あれば）とデータ保存フォルダを指定します。
 ```
# 録音時間設定値 ： 15分
# REC_TIME="00:15:00" 

# 録音データ保存フォルダを設定：絶対 PATH を指定
MY_OUTDIR="/your/directory/name/NHKロシア語講座"
 ```
2. nhkradio2-russian-record.sh にアクセス権の実行を許可します。  
 ```
 # chmod 755 nhkradio2-russian-record.sh
 ```
3. CRON に登録し毎日同時刻(8:50)に起動させます。  
\# vi /etc/crontab  
**username** は、root 或いは使用するユーザー名です（無いとエラーが出ます）。
```
# NHKまいにちロシア語：月-水【入門編】/ 木・金【応用編】8:50-9:05 (再)16:30-16:45 (前週)15:30-15:45
50 8 * * 1-5 username bash /your/directory/name/NHKロシア語講座/nhkradio2-russian-record.sh
 ```
5. CRON を再起動させます。
 ```
 # /etc/init.d/cron restart
```
※ 保存された **m4a** は音声データフォーマットであり、iTunes や通常のプレイヤーで視聴出来ます。 

# 【注意】  
録音データは著作権上私的利用のみに限定されていますのでご注意下さい。


