# Coupang Momo Matching 商品匹配
此習題使用深度學習語意模型和網頁爬蟲技術，從 MOMO 購物網擷取商品資料並與本地商品資料庫進行相似度匹配。同學可以根據需求調整搜尋詞及相似度匹配的門檻值等參數，以達成更精確的商品匹配結果。

**For NTUST EE5327701 class**

## 注意事項
所有內容與操作皆在 `scrapying_matching.ipynb` 中執行。

## 安裝與依賴
此程式使用以下 Python 套件：
- `torch`
- `numpy`
- `pandas`
- `optimum.onnxruntime`
- `onnx`
- `transformers`
- `tqdm`
- `requests`
- `beautifulsoup4`

首先，請安裝必要的套件，這些套件列在 requirements.txt 中。使用以下指令安裝所有必要的依賴：

```
pip install -r requirements.txt
```

## 功能描述

### 1. 語意模型載入

使用 `get_semantic_model()` 函數載入語意模型，用於生成商品名稱的嵌入向量，支持相似度計算。

### 2. MOMO 購物網爬蟲

`scrapy_MOMO(keyword, page, max_item_num)` 函數根據指定的關鍵字搜尋 MOMO 購物網的商品，並且將結果存成 pandas DataFrame。預設會抓取至多 `max_item_num` 個商品資料。

### 3. 商品名稱讀取

使用 `load_search_terms(filename)` 與 `load_product_data(filename)` 函數從指定檔案讀取搜尋詞及本地 CSV 商品資料，並進行商品名稱載入處理。

### 4. 嵌入向量計算

`inference(tokenizer, model, texts)` 函數將商品名稱轉為嵌入向量，用於相似度計算。

### 5. 相似度計算

`cosine_similarity(vec1, vec2)` 函數使用餘弦相似度來計算 MOMO 商品名稱與本地商品資料之間的相似程度。您可以修改 `threshold` 參數來調整匹配的相似度門檻。

### 6. 結果輸出

最終匹配的商品會按照相似度結果展示於 pandas DataFrame，其中已匹配商品顯示在最上方，未匹配商品顯示在下方。

## 使用方式

1. **語意模型載入**：預先載入模型以準備進行語意匹配。
2. **輸入檔案準備**：
   - 搜尋詞檔案 (`./queries/{student_id}_queries.txt`) 包含用於 MOMO 搜尋的關鍵詞。
   - 商品資料檔案 (`./results/{student_id}_{search_term}.csv`) 包含本地產品名稱。
3. **執行程式**：
   - 根據搜尋詞從 MOMO 爬取商品，計算嵌入向量，並與本地商品名稱進行相似度計算。
4. **檢視結果**：匹配結果會顯示於 pandas DataFrame，方便檢視匹配度高的商品。

## 參數調整

- `keyword`：可以調整 MOMO 搜尋的關鍵詞。
- `threshold`：調整相似度門檻，用於控制匹配的嚴格程度。
- `page`：設定 MOMO 爬取的頁數範圍。
- `max_item_num`：限制爬取的商品數量。
