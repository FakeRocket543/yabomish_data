# 四字熟語 / 中式流行語探索筆記

日期: 2026-04-08

## 一、中文成語增補（結論：放棄）

### 來源
- `chengyu-30310.json` (jaaack-wang) → 繁體轉換後 30,224 條
- `chinese-idioms-12976.txt` (by-syk) → 12,976 條

### 比對結果
- 現有字典 `data/chengyu_lookup.json`: 45,110 條
- 可增補: 11,522 條四字 + 551 條非四字

### 放棄原因
- 抽樣 200 條：42% 是現有成語的換字變體（如「丟盔拋甲↔丟盔棄甲」）
- 信噪比不佳，不適合直接增補
- 若需擴充建議使用教育部成語典等權威來源

---

## 二、日文四字熟語（結論：保留備用，iOS 版再用）

### 來源
- JMdict_e → 提取 `&yoji;` 標記的四字熟語

### 結果
- JMdict 標記為四字熟語: 2,073 條
- 排除萌典 + 成語詞典後: **1,598 條**
- 品質優良：「油斷大敵」「自業自得」「判官贔屓」等

### 檔案
- `doc/poc/4letters/JP/yoji-tagged-unique.txt` (1,598 條)

### 備註
- 繁中輸入法可觸發約 43% (11,003/25,098)
- 適合 iOS 鍵盤彩蛋功能，macOS 版暫不需要

---

## 三、rime-ice 簡中詞庫探索（結論：大海撈針，放棄自動篩選）

### 來源
- github.com/iDvel/rime-ice (GPL-3.0)
- base.dict.yaml (542K) + ext.dict.yaml (339K) + tencent.dict.yaml (982K)
- 合併去重: 1,861,362 條

### 篩選管線
1. rime-ice 簡體原文
2. − 台灣資料集→轉簡體（萌典 162K + 成語 45K + naer 30K = 207K）
3. − 維基詞條 (3,032K)
4. − 日文四字熟語→轉簡體
5. = **1,604,191 條**
6. jieba 自我排除組合詞 → 1,517,914 條
7. CKIP 詞性標注只留真詞 → 156,519 條
8. 只留 Na 名詞 + 去噪 → 57,519 條

### 放棄原因
- 即使經過多輪篩選，品質仍遠不如人工策展
- 大量地名、品牌名、組合詞混雜
- rime-ice 本質是通用輸入法詞庫，不是流行語詞典
- GPL-3.0 授權對閉源產品有限制

### 中間產物（留存參考）
- `data/poc/ice/cn-only.txt` (1.6M 條)
- `data/poc/ice/cn-atomic.txt` (1.5M 條)
- `data/poc/ice/cn-na-clean.txt` (57K 條)

---

## 四、中式流行語詞典（結論：採用人工策展資料）

### 來源
- `data/poc/cn_nlp/invade_vocabs.jsonl` — 374 條入侵詞（有注音、分類、例句）
- `data/poc/cn_nlp/cn_internet_slang.jsonl` — 149 條網路流行語（有年代標記）
- `data/poc/cn_nlp/cn_usage_china_side.jsonl` — invade_vocabs 的中國側補充版

### 結果
- 合併去重: **515 條**（CJK 2-6字: 533 條含簡繁兩版）
- 品質優良，有分類、釋義、例句

### 產出
- `data/poc/cn_nlp/terms_cn_slang.bin` — WBMM 格式，10.4 KB，可直接載入
- `data/poc/cn_nlp/cn_slang_dict.json` — 477 條含完整 metadata

### 分類分佈
- TECHNOLOGY 69, ADJECTIVE 62, NOUN 42, VERB 36, INTERNET 28, SLANG 26, HARDWARE 26...
- 流行語 80, 社會熱詞 16, 遊戲用語 10, 縮寫 9, 諧音梗 8, 飯圈用語 8...
