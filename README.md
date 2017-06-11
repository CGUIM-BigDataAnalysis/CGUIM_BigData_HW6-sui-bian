長庚大學 大數據分析方法 作業六
================



分析議題背景
------------

以"歷年來台旅客統計"的資料為背景，其中將旅客分為外籍旅客以及華僑旅客，可以從中得知來台旅客大多數為哪一類的，此外，以"來台旅客居住地"的資料為輔，可以分析出來來台的旅客中最多數的是來自哪個國家，甚至是哪個洲的來台的旅客最多，在"來台交通工具"的資料中，可以得知來台旅客搭乘的交通工具以及選擇著陸的地點，最後，從"中華民國國民出國目的地統計"可以得知國人出國大多去哪些地方。

分析動機
--------

希望可以從資料隨著時間的變動上觀察出那些事情會嚴重到足以間接的影響到台灣的觀光客數量，得以避免及提升台灣的觀光客數。

使用資料
--------

來自政府開放平台的
1."歷年來台旅客統計"包含外籍旅客以及華僑旅客
2."來台旅客居住地"包含亞洲地區、東南亞地區、美洲地區、歐洲地區、大洋洲、非洲地區
3."來台交通工具"包含交通工具飛機及輪船
4."中華民國國民出國目的地統計"包含亞洲地區、東南亞地區、美洲地區、歐洲地區、大洋洲、非洲地區

載入使用資料們

``` r
library(readxl)
transport <- read_excel("/Users/Jane/Desktop/CGUIM_BigData_HW6-sui-bian/來台交通工具.xlsx")
destination <- read_excel("/Users/Jane/Desktop/CGUIM_BigData_HW6-sui-bian/歷年中華民國國民出國目的地人數統計.xlsx")
country <- read_excel("/Users/Jane/Desktop/CGUIM_BigData_HW6-sui-bian/歷年來台旅客居住地統計.xlsx")
number <- read_excel("/Users/Jane/Desktop/CGUIM_BigData_HW6-sui-bian/歷年來台旅客統計.xlsx")
```

資料處理與清洗
--------------

1.將該為numeric的資料，但在data.frame裡卻是character的資料改為numeric
2.將country依據101年的的合計做排序完，列出前6名，也將100年的的合計做排序完，列出前6名，可以發現101年的前6名跟100年的前6名是一樣的國家跟順序。

處理資料

``` r
destination[[2]]= as.numeric(destination[[2]])
destination[[3]]= as.numeric(destination[[3]])
destination[[4]]= as.numeric(destination[[4]])
destination[[5]]= as.numeric(destination[[5]])
destination[[6]]= as.numeric(destination[[6]])
destination[[7]]= as.numeric(destination[[7]])
destination[[8]]= as.numeric(destination[[8]])
destination[[9]]= as.numeric(destination[[9]])
number[[3]]= as.numeric(number[[3]])
number[[5]]= as.numeric(number[[5]])
number[[8]]= as.numeric(number[[8]])
country[[9]]= as.numeric(country[[9]])
country1 = head(country[order(country[[2]],decreasing = T),])
country2 = head(country[order(country[[5]],decreasing = T),])
```

探索式資料分析
--------------

從圖中可以明顯的看出，來台灣遊玩的旅客大多都是亞洲地區的國民

``` r
library(ggplot2)
qplot(destination$`105年` ,destination$國家, data = destination)
```

期末專題分析規劃
----------------

透過"中華民國國民出國目的地統計"以及"來台旅客居住地"可以分析及推測至台灣的觀光外交部分與那些國家的關係較為友好，在"來台交通工具"中的著陸點可以推測來台的旅客大多都先去何處遊玩，希望可以從這三點中觀察出一些外交問題，或者是食安問題，甚至是發生在台灣的一些嚴重的自然災害地區是否會影響到台灣的觀光客率。
