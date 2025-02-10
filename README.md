# h2-database-introduce
一個介紹 H2資料庫 使用經驗的筆記
<br />

H2資料庫的執行環境是 jdk 11、jre 11。
<br />
詳情可參考 <a href="https://www.facebook.com/permalink.php?story_fbid=pfbid0ouw5sGNmGEjTKHkntRXCq36p2KcTJmYvgh1NRr84FL9rcqfQ4GfTx9Agn4hyHzJYl&id=100014900775688" target="_blank">這篇文章</a> 。
<br />
<br />

```no-highlight

以下皆為 Windows OS 的命令，
需打開 命令提示字元 操作。

h2資料庫 build code指令，產出能用的 jar檔
build.bat clean && build.bat compile && build.bat jar

執行 H2資料庫 啟動他的指令
h2.bat

```

<hr />
<br />

<a href="https://openhome.cc/Gossip/Spring/H2.html" target="_blank">H2 入門</a>
<br />

<a href="https://www.h2database.com/html/main.html" target="_blank">H2 Database Engine 官方網站</a>
<br />

<br />
<br />

![image](.\image\image01_messageImage_1739174170961.jpg)

<br />

接下來要分享的是怎麼設定 H2資料庫 Administrator帳號密碼，<br />
讓你可以登入『Preferences』、『Tools』這幾個介面。<br />

<br />
<br />


你可能會 Google搜尋查了查 H2中文版 教學網頁，<br />
查了很久還是沒有資料。<br />
於是去官方網站查，還是沒有資料。<br />
通靈了N個小時後。<br />
終於在胡亂搜尋 Stack Overflow 的某幾篇文章 + 自行摸索後 成功找到方法。<br />
<br />

首先這個 Administrator帳號密碼 根本無法在 GUI網頁介面做設定。<br />
你要去 H2資料庫 的 設定檔 做設定。<br />
<br />

```no-highlight

Windows OS 使用者 在這個檔案
『C:\Users\<user-name>\.h2.server.properties』
點進去這個檔案

```

<br />

```no-highlight

然後加上這個參數
『webAdminPassword=XXXX』
這個XXXX就是你的 Administrator帳號密碼

```

<br />

```no-highlight

但你以為這樣就可以了嗎？
不！並沒有！
你必須放入 hash過 的 密碼進 設定檔案 才可以！
那麼要用什麼方法 hash密碼？
你要在 Java Project 裡面引入『h2-2.3.232.jar』，
接著去呼叫 static method encodeAdminPassword() ，
然後傳入 12位碼 長度的密碼。
執行程式 產出 hash 過的 密碼。
再把該 hash密碼 複製貼上 .h2.server.properties設定檔，
關閉 H2資料庫 重新啟動 H2資料庫。
設定吃進去。

```

放一下範例程式<br />

![image](.\image\image02_messageImage_1739174863772.jpg)

<br />
<br />

接著才能成功用你設定的 Administrator帳號密碼 登入『Preferences』、『Tools』。
<br />

放一下 『Preferences』 登入畫面。<br />

![image](.\image\image03_messageImage_1739175450935.jpg)

<br />
<br />