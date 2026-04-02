# 🎓 BECE Tutor Agents — 國中會考多角色家教系統

> 五個專業 AI 教學角色，從「學→測→整→修→獎」完整陪伴國中生備考。

---

## 角色介紹

| 角色 | 徽章 | 職責 | 觸發時機 |
|------|------|------|---------|
| **講師** | 🎓 | 重點概念講解：概念地圖、生活例子、口訣 | 「我不懂」「解釋一下」 |
| **出題師** | 📝 | 設計 Anki 填充卡、選擇題、申論題 | 「考考我」「出練習題」 |
| **筆記師** | 🗒️ | 教學生提取重點、建立結構化筆記 | 「幫我整理重點」「做成筆記」 |
| **錯題師** | 🔍 | 根因分析、補救教學、Anki 驗收 | 「這題我答錯」「補救教學」 |
| **獎勵師** | 🏆 | 頒發成就徽章、追蹤進度、激勵學習 | 卡片通過、答題全對時自動觸發 |

---

## 學習流程圖

```
學生提問
  │
  ├─ 「不懂/解釋」→ 🎓 講師 主講
  │       └─ 講完 → 📝 出題師 出卡片驗收
  │               ├─ 卡片通過 → 🏆 獎勵師 頒獎
  │               └─ 卡片未過 → 🔍 錯題師 補救
  │
  ├─ 「出題/考我」→ 📝 出題師 出題
  │       ├─ 答錯 → 🔍 錯題師 解析
  │       └─ 全對 → 🏆 獎勵師 頒獎
  │
  ├─ 「整理筆記」→ 🗒️ 筆記師 整理
  │       └─ 筆記完成 → 📝 出題師 驗收
  │
  └─ 「錯題/補救」→ 🔍 錯題師 主導全流程
```

---

## 檔案結構

```
bece-tutor-agents/
├── README.md
├── .gitignore
├── bece-coach/              # 主協調器（Agent 入口）
│   └── SKILL.md
├── lecturer/                # 🎓 講師
│   ├── SKILL.md
│   └── references/
│       └── subjects.md      # 五科單元對照表
├── question-creator/        # 📝 出題師
│   └── SKILL.md
├── note-coach/              # 🗒️ 筆記師
│   └── SKILL.md
├── error-coach/             # 🔍 錯題師
│   └── SKILL.md
└── reward-coach/            # 🏆 獎勵師
    └── SKILL.md
```

---

## 涵蓋科目

- 📖 **國文**：記敘文、說明文、議論文、古文
- 🔢 **數學**：代數、幾何、統計、函數
- 🌏 **英語**：時態、句型、閱讀、寫作
- 🏛️ **社會**：歷史（台灣史/世界史）、地理、公民
- 🔬 **自然**：生物、物理、化學、地球科學

---

## 安裝到 Claude.ai

### 方法 A：上傳個別 Skill

1. 開啟 Claude.ai → 設定 → Customize → Skills
2. 上傳你需要的角色 SKILL.md（可以只上傳部分角色）
3. 確認「Code execution」已啟用

### 方法 B：上傳主協調器（推薦）

只上傳 `bece-coach/SKILL.md`，Claude 會根據學生的對話內容自動切換角色。

---

## 使用範例

```
學生：「光合作用我一直搞不懂，幫我解釋」
→ 🎓 講師上線：概念地圖 + 生活比喻 + 口訣

講師講完後自動：
→ 📝 出題師上線：出 5 張 Anki 卡片驗收

學生填完卡片（答對 4/5）：
→ 📝 出題師批改：找出錯誤點

未過關：
→ 🔍 錯題師上線：補救 + 重出補救卡

補救後通過：
→ 🏆 獎勵師上線：頒發「逆轉成功」徽章
```

---

## 參考資源

- [Anthropic Skills 官方文件](https://docs.claude.com/en/docs/agents-and-tools/agent-skills/overview)
- [Agent Skills 入門課程](https://anthropic.skilljar.com/introduction-to-agent-skills)
- [awesome-agent-skills 社群庫](https://github.com/VoltAgent/awesome-agent-skills)

---

## License

MIT — 自由使用、修改、分享。歡迎 PR 補充更多科目內容！
