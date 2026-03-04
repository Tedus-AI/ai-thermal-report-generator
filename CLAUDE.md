# ai-thermal-report-generator — Claude Code 啟動說明

## 任務概述
一個基於AI的工具，用於自動從熱影像資料生成詳細的熱分析報告，顯著提高報告生成效率和準確性。

## 開始前請依序閱讀
1. SPEC.md — 完整規格與功能清單
2. 以下 Skill 檔案：
   - .claude/skills/xlsx.md：Use this skill any time a spreadsheet file is the primary input or output. This means any task where the user wants to: open, read, edit, or fix an existing .xlsx, .xlsm, .csv, or .tsv file (e.g., adding columns, computing formulas, formatting, charting, cleaning messy data); create a new spreadsheet from scratch or from other data sources; or convert between tabular file formats. Trigger especially when the user references a spreadsheet file by name or path — even casually (like \"the xlsx in my downloads\") — and wants something done to it or produced from it. Also trigger for cleaning or restructuring messy tabular data files (malformed rows, misplaced headers, junk data) into proper spreadsheets. The deliverable must be a spreadsheet file. Do NOT trigger when the primary deliverable is a Word document, HTML report, standalone Python script, database pipeline, or Google Sheets API integration, even if tabular data is involved.
   - .claude/skills/uiux-designer-expert.md：>
   - .claude/skills/theme-factory.md：Toolkit for styling artifacts with a theme. These artifacts can be slides, docs, reportings, HTML landing pages, etc. There are 10 pre-set themes with colors/fonts that you can apply to any artifact that has been creating, or can generate a new theme on-the-fly.
   - .claude/skills/thermal-engineering-expert.md：>
   - .claude/skills/agentic-workflow.md：>
   - .claude/skills/frontend-design.md：Create distinctive, production-grade frontend interfaces with high design quality. Use this skill when the user asks to build web components, pages, artifacts, posters, or applications (examples include websites, landing pages, dashboards, React components, HTML/CSS layouts, or when styling/beautifying any web UI). Generates creative, polished code and UI design that avoids generic AI aesthetics.
   - .claude/skills/pptx.md：Use this skill any time a .pptx file is involved in any way — as input, output, or both. This includes: creating slide decks, pitch decks, or presentations; reading, parsing, or extracting text from any .pptx file (even if the extracted content will be used elsewhere, like in an email or summary); editing, modifying, or updating existing presentations; combining or splitting slide files; working with templates, layouts, speaker notes, or comments. Trigger whenever the user mentions \"deck,\" \"slides,\" \"presentation,\" or references a .pptx filename, regardless of what they plan to do with the content afterward. If a .pptx file needs to be opened, created, or touched, use this skill.

## 第一步
根據 SPEC.md 中的功能清單，從第一個 High 優先級的功能開始實作。

## 技術架構
- 前端框架：React
- 資料庫：Firebase
- 介面需求：需要 UI
- 部署平台：GitHub Pages

## 注意事項
1. **支援的相機與格式:** 假設能正確解析市面上主流熱像儀輸出的.FLIR, .IR檔案及符合規範的JPEG EXIF熱數據。2. **AI模型預訓練:** 假設AI模型已針對特定應用場景進行充分訓練，並能有效識別常見熱異常。模型更新與維護機制待後續定義。3. **計算資源:** 假設部署環境具備足夠的CPU/GPU和記憶體，以支援熱影像處理及AI模型推斷。4. **輸入數據品質:** 假設使用者提供的環境參數和物件資訊是準確且能代表實際狀況的。5. **報告模板彈性:** 預設提供多個標準報告模板，使用者自定義模板功能可能在初期版本中有限或有特定格式要求。6. **影像數量與時序:** 初期版本可能聚焦於單一影像或少量影像批次處理。若需進行長期趨勢預測，需使用者提供一系列帶時間戳的熱影像。7. **系統擴展性:** 初期設計優先滿足核心功能，大規模數據處理或高併發訪問的擴展性將在後續階段考量。

邊界條件：1. **輸入檔案完整性:** 熱影像檔案損壞或無法解析，系統應提供錯誤提示。2. **EXIF數據缺失:** JPEG檔案若不含足夠的熱數據EXIF資訊，則無法進行熱分析，應提示使用者。3. **參數有效性:** 發射率（Emissivity）必須在0.0到1.0之間；環境溫度（Ambient Temperature）應在合理範圍內（例如-50°C到100°C）。若關鍵參數缺失，系統應使用預設值或提示使用者補齊。4. **影像內容極端情況:** 熱影像完全均勻、對比度極低、或包含多個複雜交疊的物件時，可能影響分析準確性。5. **處理時間:** 單次分析的熱影像數量與解析度應設有上限，以避免因單次任務過重導致超時。
