# InfraDocs Coach｜AI 基礎設施文件助教

生成式 AI 課程 RAG 作業：以 vLLM **v0.11.0 固定版本**的 prefix caching 官方文件建立可引用來源的繁體中文問答機器人。

- **RAG01**：下載原文 → 依章節及 token 切塊 → multilingual-e5-small 向量化 → FAISS → `rag-data.zip`。
- **RAG02**：從公開固定版本網址下載 ZIP → 檢索 → AISuite / Groq 回答 → Gradio 展示。

| 筆記本 | 用途 | 開啟 |
| --- | --- | --- |
| RAG01 | 建立資料庫，輸出 `rag-data.zip` | [Open in Colab](https://colab.research.google.com/github/seankohjs/genaimod-rag-infradocs/blob/ad74dce7676c0bcbe1070fb739488eeb5e094d33/RAG01_InfraDocs_%E5%BB%BA%E7%AB%8B%E8%B3%87%E6%96%99%E5%BA%AB.ipynb) |
| **RAG02** | **繳交用：下載 ZIP、文件問答及 Gradio** | [Open in Colab](https://colab.research.google.com/github/seankohjs/genaimod-rag-infradocs/blob/ad74dce7676c0bcbe1070fb739488eeb5e094d33/RAG02_InfraDocs_%E5%B0%8D%E8%A9%B1%E6%A9%9F%E5%99%A8%E4%BA%BA.ipynb) |

## 執行方式

1. 開啟 RAG02，選「檔案 → 在雲端硬碟中儲存副本」。
2. 在左側 Secrets 新增 **`Groq`**，貼上自己的 API key 並開啟此筆記本的存取權。
3. 執行全部儲存格，CPU 即可。若安裝後要求重新啟動，照提示重啟再從頭執行。
4. 在 Gradio 提問；「只看檢索」不需金鑰，「依文件回答」會呼叫 Groq。
5. 閱讀右側原文核對引用，填寫第 7 節的實測觀察，再分享自己的 Colab 副本。

兩份皆保留課程固定四行套件。RAG01 不需要 API key；RAG02 使用 AISuite 與 Groq `openai/gpt-oss-20b`，金鑰不寫入程式。
問題、必要近期對話與相關原文片段會傳至 Groq；對話保留最近四輪，每個 Gradio session 分開處理。

下載資料庫不需要登入：[固定版本 rag-data.zip](https://raw.githubusercontent.com/seankohjs/genaimod-rag-infradocs/de21d3dbb6c45aeb43d0e5ded19f5be41593eaec/rag-data.zip)。
SHA256：`275f2a490da9df10123953df09d4cb35560bbc0b6a063570f9139475d1440864`。
RAG02 已內建此網址與驗證值，不需手動上傳。ZIP 以 FAISS + JSON 儲存，未使用 Python pickle。

## 本機驗證範圍

2026-10-31 在 macOS / Python 3.12 環境中，兩份 notebook 各 7 個程式儲存格皆執行成功。
RAG02 從空白工作目錄下載本儲存庫的公開 ZIP；五個繁體中文問題在前四名找到對應英文依據，另有 V0 追問檢索檢查。
Gradio 的實際向量檢索、清除對話與缺少金鑰提示已測試；AISuite / Groq 請求格式以明確標記的 HTTP 替身測試。
**尚未在學生 Colab 內使用真實 Groq 金鑰測試生成回答**，筆記本第 7 節因此保留待填欄位。
保留的表格是實際檢索輸出，未放入假冒的 LLM 回答；已移除失效的本機介面及純本機診斷路徑。

RAG 的引用提示不是事實保證；請核對原文是否支持回答，尤其是部署效能或文件範圍以外的問題。

## 資料與來源

兩個章節來自同一份 vLLM 文件集，固定於 commit `b8b302cde434df8c9289a2b465406b47ebab1c2d`：

- [Automatic Prefix Caching 使用說明](https://github.com/vllm-project/vllm/blob/b8b302cde434df8c9289a2b465406b47ebab1c2d/docs/features/automatic_prefix_caching.md)
- [Prefix Caching 設計說明](https://github.com/vllm-project/vllm/blob/b8b302cde434df8c9289a2b465406b47ebab1c2d/docs/design/prefix_caching.md)

包含 22 個原文片段、384 維向量；每塊最多 280 tokens，重疊 48 tokens。原文為英文，問題及回答使用繁體中文。
圖片與外連範例未納入索引。這個資料庫用於固定版本的學習，並不涵蓋 vLLM 全部功能或最新版本。

向量模型為 [intfloat/multilingual-e5-small](https://huggingface.co/intfloat/multilingual-e5-small)，固定 revision `614241f622f53c4eeff9890bdc4f31cfecc418b3`。
文件使用 `passage: `、查詢使用 `query: ` 前綴，L2 正規化後以 FAISS 內積搜尋。

## 授權與致謝

vLLM 文件採 Apache-2.0；ZIP 內保留原文及 `LICENSE-vllm.txt`。新撰寫的程式與說明採本儲存庫 MIT 授權，原始文件依其自身授權。
流程參考老師的 [RAG01](https://github.com/yenlung/AI-Demo/blob/master/【Demo06a】RAG01_打造向量資料庫.ipynb) 與 [RAG02](https://github.com/yenlung/AI-Demo/blob/master/【Demo06b】RAG02_打造_RAG_系統.ipynb)。
AI 協助選題、Prompt、程式實作與驗證；個人測試觀察及課程繳交由學生完成。
