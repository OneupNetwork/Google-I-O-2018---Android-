# Google-I-O-2018---Android-
稍微整理了一下今年 Google I/O Android 部分的新內容給大家參考
Google I/O Android 部分整理
(參考資料: https://android-developers.googleblog.com/2018/05/google-io-2018-whats-new-in-android.html)

1. JETPACK : 一連串針對Android 開發，架構及介面上的強化功能 library 及元件，包含 

* KTX：提供幾個 Kotlin 開發上方便使用的 library ，library 中能讓程式開發上省略掉很多不必要的 boilerplate的方法，例如資料庫的 transaction，原本需要寫一些固定的code來開始 transaction 及結束，這邊 KTX就有提供簡化這個流程的方法
      ![](https://i.imgur.com/5DKHGXB.png)
      
     或是像下面這個簡單能處理 span 的方法也是 KTX 中提供的功能
      ![](https://i.imgur.com/zw5xZKg.png)


* Room：Android 資料庫的 SQL mapping library，能夠更簡單的定義資料庫中 table欄位，操作動作等，也對 SQL query 有檢查機制，防止開發時錯誤的 SQL 語法，提供了同步及非同步的操作處理

  ![](https://i.imgur.com/zPkxwLs.png)

  ![](https://i.imgur.com/LiE7Fq6.png)

  ![](https://i.imgur.com/XF81Lzd.png)


* ViewModel：可以在 configuration changed 時完整保留所有頁面上的資料的 data object，以下是他與 onSavedInstance 方法使用上的不同，主要不同是他可以儲存大量的資料，讓畫面改變時能夠不需要重新載入資料
 
  ![](https://i.imgur.com/4sHKAcK.png)
  
  ![](https://i.imgur.com/cX6HjkI.png)
  
  ![](https://i.imgur.com/bLmVTT8.png)

* LiveData：Observable 的 dataholder，通常會搭配 ViewModel 及 DataBinding 使用，可以達到資料更新時自動更新 UI畫面而且具有 Lifecycle aware 的特性，所以在 像是 Activity destroyed 時就不會再去試圖更新畫面

  ![](https://i.imgur.com/VBH8LwB.png)

  ![](https://i.imgur.com/wrWgoxl.png)

  ![](https://i.imgur.com/WF2g6aP.png)


* Paging Library：可搭配 Recycler 及 LiveData 使用，在很多 App 中都需要針對一整個 list 的資料做分頁讀取，Paging library 就提供了簡化這個流程的方法。

  分為 PagedList 及 DataSource 兩個部分，DataSource 可讀取各種來源的資料，下面這張圖解釋了整個讀取資料的流程，會自動從 DataSource 讀取資料更新到 UI 上，有提供 PagedListAdapter 可達到自動一段一段更新到畫面上的處理，如果資料讀取完了，會有 BoundaryCallback，假設原本是從 DB讀取資料這時可以在這個地方去拉 Network的資料回來，再繼續流程。
  另外還可以搭配 Room，Room可以回傳 DataSourceFactory 的資料方便這整個流程進行
![](https://i.imgur.com/YBeIJcz.png)


* AutoSizingTextView：新的元件，可自動在 TextView size 改變時去調整字體大小
  使用方法是在 xml 設定 
  `android:autoSizeTextType="uniform"` 
  這邊要注意的是不要使用 wrap_content，可能會造成一些問題，他可以設定最大/最小的字體大小，還可以預設只有縮放到哪些大小(Preset size) 
  
* EmojiCompat：解決 Emoji 不存在的問題，以 EmojiSpan 取代那些系統找不到的 Emoji font，也可以讓 custom emoji 更方便的實作
![](https://i.imgur.com/hA8npC8.png)


2. Android App Bundle：(beta program)
在Google play 後台上傳 App bundle，應是取代傳統 apk上傳，優點是使用者在下載 app 時，能夠只下載需要的部份，例如當他的手機是小手機，那大 resolution 的資源就不下載

3. Google play console 優化
4. Slices 及 Action：
   Action(https://developer.android.com/guide/actions/) 
   是 Google 對Android 介面及 google 搜尋介面上的更新，在例如像是使用者選取文字時，能夠自動提供相對應的 app 建議(尚未正式推出)，如下圖 ![](https://i.imgur.com/X0FKFxP.png)
   
   而Slices (https://developer.android.com/guide/slices/getting-started)
   則是 developer需要在 app 中實作的部份，在 Action 提供建議時能提供更細的 app 功能，例如使用叫車 app，在 Action 顯示建議時能透過 Slices 連帶顯示詳細的車資計算等等資訊，讓使用者能更快更直接的使用到 app 細部的功能



