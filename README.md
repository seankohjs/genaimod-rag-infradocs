# InfraDocs Coach｜AI 基礎設施文件助教

生成式 AI 課程 RAG 作業：以 vLLM **v0.11.0 固定版本**的 prefix caching 官方文件建立可引用來源的繁體中文問答機器人。

- **RAG01**：下載原文 → 依章節及 token 切塊 → multilingual-e5-small 向量化 → FAISS → `rag-data.zip`。
- **RAG02**：從公開固定版本網址下載 ZIP → 檢索 → AISuite / Groq 回答 → Gradio 展示。

完整筆記本及 Colab 開啟連結會放在此處。下載資料庫不需要登入。

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
