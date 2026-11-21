請依照 Andrej Karpathy 的 LLM Wiki 架構（https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f），幫我在 Codex 建立「馬光醫療網工作知識庫」。全程使用繁體中文，逐步完成以下五個步驟，每完成一步用一行回報。

## 第一步：下載知識庫範本

範本網址：https://github.com/blackrocx0/maguang-llm-wiki

1. 如果目前資料夾裡已經有 `AGENTS.md` 和 `raw/`，代表下載過了，直接跳到第二步。
2. 否則在目前資料夾建立子資料夾 `maguang-llm-wiki`，用 git 下載：
   `git clone --depth 1 https://github.com/blackrocx0/maguang-llm-wiki.git maguang-llm-wiki`
3. 如果電腦沒有 git，改下載壓縮檔並解壓縮成 `maguang-llm-wiki` 資料夾：
   - Windows（PowerShell）：
     `Invoke-WebRequest -Uri "https://github.com/blackrocx0/maguang-llm-wiki/archive/refs/heads/main.zip" -OutFile "maguang.zip"; Expand-Archive "maguang.zip" -DestinationPath "."; Rename-Item "maguang-llm-wiki-main" "maguang-llm-wiki"`
   - macOS（終端機）：
     `curl -L -o maguang.zip https://github.com/blackrocx0/maguang-llm-wiki/archive/refs/heads/main.zip && unzip -q maguang.zip && mv maguang-llm-wiki-main maguang-llm-wiki`
4. 下載需要網路，如果跳出權限確認，請提醒我按「允許」。

之後所有操作都在 `maguang-llm-wiki` 資料夾內進行。

## 第二步：讀懂規則

閱讀 `AGENTS.md`，以及 `.agents/skills/` 底下四個技能（ingest、query、lint、capture）的 `SKILL.md`，之後所有動作都照這些規則執行。用 3 行向我說明這個知識庫的三層架構。

## 第三步：第一次 Ingest

依照 `.agents/skills/ingest/SKILL.md`，把 `raw/` 的全部素材（約 38 份，包含會議紀錄、SOP、LINE 群組對話、Email、客訴紀錄、CSV 報表）消化進 `wiki/`。分批處理，每批完成後回報一行進度。完成後確認：
- `wiki/index.md` 已依分類列出所有頁面
- `wiki/log.md` 每份素材都有一筆 INGEST 紀錄
- 列出你發現的規則衝突與待確認事項（不同文件說法不一致的地方）

## 第四步：示範一次問答

依照 `.agents/skills/query/SKILL.md` 回答：「病人想取消預約，最晚什麼時候要通知？各院規定一樣嗎？明年會不會改？」
回答要標注引用頁面，並說明哪些部分目前還在待確認。

## 第五步：說明使用方式

用以下格式回報：

```
✅ 馬光 LLM Wiki 建置完成！

## 📁 你的知識庫結構
[列出 raw/ 素材數量、wiki/ 頁面數量，並依分類列出 wiki 頁面]

## 🏥 本次素材
馬光醫療網各職務的模擬工作情境：櫃台與 CRM、跟診與藥局、院所營運、總部行銷、人資訓練、醫務行政與健保（人物、院所、數據皆為虛構）

## 🚀 四個核心技能
| 技能 | 用途 | 範例 |
|------|------|------|
| `$ingest`  | 消化新素材進 wiki | `$ingest` 或 `$ingest raw/我的筆記.md` |
| `$query`   | 向知識庫提問 | `$query 新人訓練要幾天？` |
| `$lint`    | 健康檢查 wiki | `$lint` |
| `$capture` | 把對話中的新資訊收錄進 raw/ | 自動判斷，不用特別輸入 |

## 📖 建議的使用流程
1. 下次開 Codex 時，選擇 `maguang-llm-wiki` 資料夾作為專案，規則和技能會自動載入（輸入 `$` 可以看到技能清單）
2. 把你的 SOP、會議紀錄、公告（先去掉病患個資）放進 `raw/`，執行 `$ingest`
3. 有問題直接問，或用 `$query`
4. 每週跑一次 `$lint`，抓出矛盾、過時內容與個資問題

## 💡 小技巧
- 直接告訴我新消息，例如「北一院下個月起初診要多填一份問卷」，我會自動判斷要不要收錄進 raw/ 並更新 wiki
- 好的問答會存回 wiki 的「問答沉澱」，越用越聰明
- `wiki/index.md` 是你的知識地圖，`wiki/log.md` 記錄所有操作歷史
- 不要把病患姓名、電話、病歷號放進知識庫

立即體驗：輸入 `$lint`，看看 AI 能不能抓出這些文件裡藏著的矛盾與過時規定！
參考原始設計：https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f
```

請開始執行，逐步完成以上五個步驟。
