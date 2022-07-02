# Machine Learning Note

###### tags: `machine learning` `project`

## 人工智慧的分級
- 依照處理及判斷區分四個類別

### 第一級: 自動控制
經由感測器偵測環境的資訊，去做出某些特定動作以達成自動控制

- 透過溫度感測器偵測是否過熱，決定是否停止運轉
- 冷氣低於20度時，進入待機模式

> 好比是公司裡的工讀生：只是執行老闆交待的命令，做各種重複性的工作
> 例如：老闆說把大箱子搬到寫有「大」的區域 [color=#7cba25]

:::info
:bulb: **HINT** 此時程式設計師必須先把所有可能的情況都考慮進去才能寫出控制程式

![image alt](https://ithelp.ithome.com.tw/upload/images/20210921/20107247qJq9CdDAgC.png)
:::

### 第二級: 探索討論
強調邏輯推理，制定好一套知識庫與規則庫後，
讓機器產生大量輸入與輸出資料的排列組合來解決日常生活中的問題

- 掃地機器人
- 回答問題的人工智慧

> 好比是公司裡的員工：能夠理解老闆交待的規則並且做出判斷 
> 例如：根據箱子長、寬、高分類大小箱子 [color=#7cba25]
:::info
![image alt](https://ithelp.ithome.com.tw/upload/images/20210921/20107247O3npJy6NR8.png)
:::

### 第三級: 機器學習
根據資料學習如何將輸入與輸出資料產生關聯

- 搜尋引擎
- 大數據分析

> 好比是公司裡的經理：能夠學習原則並且自行判斷
> 例如：老闆給予判斷原則（特徵值），讓經理自己學習以及透過以前經驗判斷多大是大箱子？[color=#7cba25]

:::info
:bulb: **HINT** 學習方式可大致分為監督式學習、非監督式學習、增強式學習，此外自監督學習這個名詞最近也熱烈的討論中
:::

### 第四級: 深度學習
電腦可以自行學習並且理解機器學習時用以表示資料的「特徵值」，因此又稱為「特徵表達學習」

- 影像分類
- 機器翻譯

> 好比是公司裡的總經理：能夠發現規則並且做出判斷
> 例如：發現有一個箱子雖然很大但是卻是圓形（特徵值），與其他貨物不同應該另案處理 [color=#7cba25]

:::info
![image alt](https://ithelp.ithome.com.tw/upload/images/20210921/20107247LthVZkdrnv.png)
:::


## 機器如何學習？

### a. 監督式學習 Supervised Learning
給許多資料並給與答案，透過損失函數計算來找出一個最佳解

:::info
**比如** 給機器各看了 1000 張貓和狗的照片後再詢問機器新的一張照片中是貓還是狗。

![image alt](https://ithelp.ithome.com.tw/upload/images/20210921/20107247tYOrjOLQXt.png)
:::


### b. 非監督式學習 Unsupervised Learning
只給定特徵，機器會想辦法會從中找出規律，最常見的方法就是集群分析(Cluster Analysis)

:::info
:bulb: **HINT** 給許多資料但不給予答案，模型會從資料中自己去找出關係

![image alt](https://ithelp.ithome.com.tw/upload/images/20210921/201072476K74tSRkyg.png)
:::

### c. 半監督式學習 Semi-Supervised Learning
利用好未標記樣本來提升模型泛化能力

:::info
:bulb: **HINT** 應用主要在於收集資料很簡單，但標記的資料太少( 比較普遍現象 )

![](https://ithelp.ithome.com.tw/upload/images/20210921/20107247VT57PA24r7.png)
:::

### d. 強化式學習 Reinforcement Learning
會進行一系列的動作，而每做一個動作、環境都會跟著發生變化
機器透過不斷的從錯誤中去學習，最終學到了如何去解決一件事情

:::info
:bulb: **HINT** 若環境的變化是離目標更接近，我們就會給予一個正向反饋，反之，則給予負向反饋

![](https://ithelp.ithome.com.tw/upload/images/20210921/20107247NSiNhkMHBW.png)
:::

### e. 自監督學習 Self-Supervised Learning
透過當前任務觀察所得到的特徵，並訓練一個目標任務的模型，且過程中不仰賴人類給定的標籤

:::info
:bulb: **HINT** 訓練過程是拿一個訓練好的模型透過非監督式技巧 pre-text task 訓練好模型
                訓練完成後再接到下游任務做最後的模型微調 (fine tune)
                
![](https://ithelp.ithome.com.tw/upload/images/20210921/20107247wc0qxYYguH.png)
:::

