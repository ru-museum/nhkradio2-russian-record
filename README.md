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
REC_TIME="00:15:00" 

# 録音データ保存フォルダを設定：絶対 PATH を指定
MY_OUTDIR="/your/directory/name/NHKロシア語講座"
 ```
2. nhkradio2-russian-record.sh にアクセス権の実行を許可します。  
 ```
 # chmod 755 nhkradio2-russian-record.sh
 ```
3. CRON に登録し毎日(月-金)同時刻(8:50)に起動させます。  
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
### 録音開始時間の微調整  
- 回線状況や配信（放送時刻）とPCの時計の時刻が正確に合致していない場合など、録音開始時間に**誤差**の生じる場合があります。  
- 当方の PC の内蔵時計では日本標準時との誤差は 0.2 秒でしたが、**36秒**の遅延調整が必要でした。  
　　[情報通信研究機構/日本標準時](https://www.nict.go.jp/JST/JST5.html)

**(A)** 開始時刻を遅らせる場合：録音開始時間調整の　**sleep** の値を変更します（初期値：0）。  
　例：開始時刻を**36秒**遅らせる
```
sleep 36　  
```
**(B)** 開始時刻を早める場合（稀なケース）： CRON で行います（CRON の再起動が必要）。  
　例：録音開始時刻を**20秒**早める：開始時刻を**1分**早め（初期値：50 ⇒ 49）開始時刻まで**40秒** sleep させます。
```
49 8 * * 1-5 sleep 40; username bash /your/directory/name/NHKロシア語講座/nhkradio2-russian-record.sh
```

※ 保存された **m4a** は音声データフォーマットであり、iTunes や通常のプレイヤーで視聴出来ます。 

# 【注意】  
- 配信 URL は時期は不明ですが変更されています。  
旧URL: "https://nhkradioakr2-i.akamaihd.net/hls/live/511929/1-r2/1-r2-01.m3u8"  
新URL: "https://radio-stream.nhk.jp/hls/live/2023501/nhkradiruakr2/master.m3u8"
- 録音データは著作権上私的利用のみに限定されていますのでご注意下さい。


