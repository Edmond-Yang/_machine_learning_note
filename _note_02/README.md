
### Modules
* 資料處理
  * Pandas：Python 表格資料處理的重要工具
  * Numpy：針對多維陣列的平行運算進行優化的強大函式庫
* 繪圖相關
  * Matplotlib：Python 最常被使用到的繪圖套件
  * Seaborn：以 matplotlib 為底層的高階繪圖套件
* 資料來源
  * Sklearn：提供鳶尾花 (iris) 的相關資料


```python=

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.datasets import load_iris

```

#### 載入資料
- Sklearn ( sklearn.datasets )
  - load_iris( ) : 載入 iris 的資料
    - data : 輸入資料
    - target : 輸出資料

```python=

iris = load_iris()
x = iris.data
y = iris.target
print('x:', type(x), '(150, 4)')
print('y:', type(y), '(150, )')

```

- Pandas
  - DataFrame : 將資料轉成表格
    - data : 資料
    - columns : 對應的變數名
- Numpy
  - c_[ ] : 將array左右合併在一起

```python=

df_iris = pd.DataFrame(data=np.c_[iris['data'], iris['target']])
df_iris.columns = ['SepalLengthCm','SepalWidthCm','PetalLengthCm','PetalWidthCm','Species']
print(df_iris)

```

### EDA (Exploratory Data Analysis) 探索式資料分析
主要概念是透過數據統計的方式視覺化資料。做EDA的好處可以從各種面向先了解資料的狀況，以利後續的模型分析。
#### 直方圖
- Pandas
  - DataFrame.hist() : 建立長方圖
    - alpha : 顏色透明度
    - layout : 圖表排版的數量 tuple (rows, columns)
    * [ figsize ] : 圖表大小
    * [ bins ] : 長方的數量
- Matplotlib
  - tight_layout() : 讓 plot 自動保持子圖之間的正確間距
  - show() : 印出圖表們

```python=

df_iris.hist(alpha=0.6,layout=(3,3), figsize=(12, 8), bins=10)
plt.tight_layout()
plt.show()

```
- Matplotlib
  - subplots( ) : 創建視窗以及子圖物件
    - nrows, ncols : 行列的圖表數量
    - fig : 小視窗
    - axes : 圖形物件
- Seaborn
  - histplot( ) : 創造長方圖
    - data : 資料
    - ax : 圖形物件
    - kde : 核密度估計 -> 將長條圖轉成折線圖
- df_iris \[ " SepalLengthCm " \] \[ : \] -> 複製 list, array 來用

```python=

fig, axes = plt.subplots(nrows=1,ncols=4)
fig.set_size_inches(15, 4)
sns.histplot(df_iris["SepalLengthCm"][:],ax=axes[0], kde=True)
sns.histplot(df_iris["SepalWidthCm"][:],ax=axes[1], kde=True)
sns.histplot(df_iris["PetalLengthCm"][:],ax=axes[2], kde=True)
sns.histplot(df_iris["PetalWidthCm"][:],ax=axes[3], kde=True)

```
### 核密度估計 Kernel Density Estimation(KDE)
- 核密度估計 KDE
  - 對角線部分
    - 核密度估計圖 : 某一個特徵的分佈情況
      - x軸 : 對應著該特徵的數值
      - y軸 : 對應著該特徵的密度，也就是特徵出現的頻率
  - 非對角線部分
    - 兩個特徵之間分佈的關聯散點圖

- Pandas.plotting
  - scatter_matrix( ) : 繪製散佈圖
    - frame : 資料 ( pandas DataFrame )
    - figsize : figure 大小
    - color : 顏色
    - diagonal : 對角線呈現 hist 或 kde

```python=
from pandas.plotting import scatter_matrix
scatter_matrix( df_iris,figsize=(10, 10),color='b',diagonal='kde')

```

- Seaborn
  - pairplot( ) : 繪製多個成對的雙變量分布
    - data : 資料
    - hue : 在 data 中的不同變數映射到不同顏色
    - height : 刻度高度
    - diag_kind : 對角線部分為 hist, kde, auto, None

```python=
sns.pairplot(df_iris, hue="Species", height=2, diag_kind="kde")

```

- dict \[ \[ keys ] ] : 意指只包含 keys 們以及對應 value 們的 dict
* 下面程式兩者是一樣的

```python=
print(df_iris[['SepalLengthCm','SepalWidthCm','PetalLengthCm','PetalWidthCm','Species']])
print(df_iris)

```
- Pandas
  - dataframe.corr() : 配對的關聯係數
- Seaborn
  - heatmap() : 熱點圖
    - data : 資料
    - square : 圖須為正方形
    - annot : 顯示比值在圖中
    - cmap : matplotlib colormap name

```python=
# correlation calculate
corr = df_iris[['SepalLengthCm','SepalWidthCm','PetalLengthCm','PetalWidthCm','Species']].corr()
plt.figure(figsize=(8,8))
sns.heatmap(corr, square=True, annot=True, cmap="RdBu_r") #center=0, cmap="YlGnBu"
```
- Seaborn
  - lmplot( ) : 繪製迴歸圖
    - x, y : 資料中的兩個變數
    - hue : 在資料中的不同變數映射到不同顏色
    - data : 資料
    - fit_reg : 估計出兩者迴規模型
    - legend : 圖例
- Matplotlib
  - legend( ) : 圖例
    - title : 標題
    - loc : 位置
    - labels : 對應的標籤

```python=
sns.lmplot("SepalLengthCm", "SepalWidthCm", hue='Species', data=df_iris, fit_reg=False, legend=False)
plt.legend(title='Species', loc='upper right', labels=['Iris-Setosa', 'Iris-Versicolour', 'Iris-Virginica'])

```
### 箱型圖
透過箱形圖可以分析每個特徵的分布狀況以及是否有離群值
```python=
fig, axes = plt.subplots(nrows=1, ncols=5, figsize=(10,5), sharey=True)
axes[0].boxplot(df_iris['SepalLengthCm'],showmeans=True)
axes[0].set_title('SepalLengthCm')

axes[1].boxplot(df_iris['SepalWidthCm'],showmeans=True)
axes[1].set_title('SepalWidthCm')

axes[2].boxplot(df_iris['PetalLengthCm'],showmeans=True)
axes[2].set_title('PetalLengthCm')

axes[3].boxplot(df_iris['PetalWidthCm'],showmeans=True)
axes[3].set_title('PetalWidthCm')

axes[4].boxplot(df_iris['Species'],showmeans=True)
axes[4].set_title('Species')
```
