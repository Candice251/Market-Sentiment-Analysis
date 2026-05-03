# 財經新聞情緒偵測與市場應用
> 程式碼與完整說明文件詳見下方連結。

- 新聞文章情緒偵測.pdf: 詳細結果報告
- all-data.csv: kaggle 資料 Sentiment Analysis for Financial News
- yahoo_finance_data.csv: Yahoo Finance 新聞資料
- yahoofinance_data.ipynb: 抓取 Yahoo Finance News
- Preprocessing&Training.ipynb: 資料前處理與模型訓練
- Yahoo_Finance_BERT.ipynb: 應用 Yahoo Finance News 並與 S&P 500 指數結果比較

## 專案簡介
以 kaggle 財經新聞資料集微調 BERT 情緒分類模型，
並將模型應用於 S&P 500 前 100 大成分股的即時新聞，
驗證新聞情緒指標與市場股價、日報酬率的相關性，
發現昨日極端情緒對今日報酬率具備反向預測潛力。

## 技術棧
- **語言**：Python
- **模型**：BERT（bert-base-uncased）、TF-IDF + Logistic Regression
- **NLP**：Transformers, scikit-learn
- **資料爬取**：yfinance
- **視覺化**：Matplotlib, Seaborn

## 核心方法
- 資料處理：Stratified Split 處理類別不平衡（中立佔 59.4%）、自定義 Stopwords 過濾財經雜訊詞
- 建模：以 TF-IDF + LR 建立 Baseline，微調 BERT 進行三分類（正向／中立／負向）
- 市場應用：計算 S&P 500 成分股每日平均情緒分數，與股價點數及日報酬率進行相關性檢定
- 時間平移分析：將情緒指標 Shift +1 Day，檢驗 T-1 情緒對 T 日報酬的預測效力

## 主要結果

| 分析對象 | 相關係數 | 解讀 |
|---------|---------|------|
| BERT 準確率 | 84.23% | 較 Baseline 提升 12.79% |
| 當日情緒 vs. 股價點數 | +0.61 | 情緒與市場趨勢同步 |
| 當日情緒 vs. 日報酬率 | -0.09 | 無顯著關聯 |
| 昨日情緒 vs. 日報酬率 | **-0.61** | 極端情緒具反向預測潛力 |

> ⚠️ 市場應用部分觀測期間為 7 個交易日（N=7），結論具初步參考價值，尚待更長期資料驗證。

## 完整說明
詳見 PDF 文件
