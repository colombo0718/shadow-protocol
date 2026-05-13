# PROJECT.md — Shadow Protocol（暗影協定）

## 這是什麼

**Shadow Protocol** 是 LeafLune 戰術空間（SS）旗下的**潛行策略 × 資訊安全 × AI 教育**同步回合制策略遊戲。

玩家操控數位戰場上的智能程式、在光明與陰影之間進行攻防：忍者的潛行、守衛的掃描、陷阱的佈置——這些都是真實的資安攻防演算法模擬。

**不只是遊戲、是讓學生自然理解加密、入侵偵測、AI 策略的互動學習環境**。

---

## LL 三軸定位

- **空間軸**：對外（SS 子產品、有用戶會玩）
- **時間軸**：未來 → 現在（MVP v0.1 開發中、Live Demo 可玩）
- **內容軸**：玩樂 × 學習（Edutainment 中間偏玩樂）

**所屬品牌**：SS（Strategy Space 戰術空間）旗下、不是獨立平台。

---

## 線上 Live Demo

🕹️ <https://shadow-protocol-bice.vercel.app/>

---

## 架構概覽

```
shadow-protocol/
├── CLAUDE.md       通用員工手冊（從 MM 複製）
├── PROJECT.md      本檔
├── README.md       對外介紹（給玩家 / 訪客）
├── TODO.md         待辦 + ⬡ MM 同步表
├── cover.png       封面圖
├── index.html      主遊戲入口（current）
├── cyberBlockly.html   Blockly 編輯器頁面
├── show-grid.html  網格除錯頁
│
├── docs/           硬約束文件（規格、改了會壞）
│   ├── ShadowProtocol_MVP_v0.1.md
│   ├── Shadow Protocol｜控制模式與可見性規格（Final Draft）.md
│   ├── ShadowProtocol_Mode_Visibility_Spec.md
│   └── ShadowProtocol_ProgramSystem.md
│
├── notes/          軟敘述（世界觀、設計想法、白皮書）
│   ├── Shadow_Protocol_世界觀與系統總覽.md
│   ├── ShadowPath_陰影之路.md
│   ├── ShadowProtocol_MirrorModes.md
│   ├── Shadow_Protocol_Whitepaper_v2.0.md
│   └── 💠 Cyber Protocol：暗影協定.md
│
└── archive/        歷史備份（舊版 HTML / 不再使用文件）
    ├── LL_Universe_MasterPlan_v1.md（應去 MM 看最新版）
    ├── index_20251108.html
    └── index_20260401.html
```

---

## 核心玩法（從 README 提煉）

### 同步回合制（Simultaneous Turns）
玩家與 AI 同時提交行動、同時結算——消除等待感、製造策略張力。

### 光影系統
- **陰影格**：加密通道、程式完全隱身
- **光照格**：開放通道、暴露在掃描下
- 熄燭 / 投石 / 設陷影響戰場光影格局

### 聽覺系統
聲音穿牆傳播、不同動作不同聲源半徑、可洩露位置也可製造誘餌。

### 三種控制模式

| 模式 | 說明 | 提示符 |
|------|------|--------|
| **直控 Direct** | 按鍵即行動、適合新手 | `:` |
| **指令 Command** | 一次規劃 N 步、提交後執行 | `>` |
| **腳本 Script** | Blockly 積木撰寫 AI 自動行為 | `$` |

---

## 開發現況

- **MVP v0.1**：直控模式 + 開燈環境 + 10×10 網格、可移動 / 熄燭 / 撿卷 / 抵達出口
- **規格詳見** [`docs/ShadowProtocol_MVP_v0.1.md`](docs/ShadowProtocol_MVP_v0.1.md)
- **Live Demo** 部署在 Vercel（[shadow-protocol-bice.vercel.app](https://shadow-protocol-bice.vercel.app/)）

---

## 演進方向：Agentic Curriculum

> 2026-05-13 浮現的戰略方向、未來 PoC 起點

Shadow Protocol 的離散網格 + 元件少 + 規則清楚的結構、**完美適合**「Generator + Tester」對抗式關卡生成架構：

```
Generator Agent  →  生成 10×10 關卡（牆/燭/卷/出口配置）
       ↓
Tester Agent    →  BFS/A* 求解、量化難度分數
       ↓
Curriculum Curator → 100 關按難度排序、形成階梯
       ↓
玩家體驗            → 不是手刻關卡、是 AI 生成 + 階梯化的 curriculum
```

**教育意義升級**：
- 玩家玩 SP 的同時、體驗 PCGML（Procedural Content Generation via ML）
- 跟 RR（強化教室）的 curriculum learning 教學主線**完美呼應**
- 老師可指著遊戲說：「這 30 關不是手刻、是 AI 設計階梯化的結果」

落地三階段：
- **Phase 0** PoC：純 Python 寫 Generator + Tester、跑 100 關、看難度分布（1 週）
- **Phase 1**：整合進 SP MVP、玩家實玩驗證體感（2 週）
- **Phase 2**（可選）：對抗式迭代、Generator 學會生「有趣」關卡

詳細任務見 [`TODO.md`](TODO.md)。

---

## 已知坑 / 注意事項

- `index.html` 跟 `archive/index_20260401.html` 內容完全相同（後者是備份）
- `archive/LL_Universe_MasterPlan_v1.md` 是舊版 LL 總藍圖、**已過時**、最新版請去 `matrix-manager/UNIVERSE.md`
- `CLAUDE.md` 從 `matrix-manager/CLAUDE.md` 同步複製、不可自己改寫

---

## 部署

- 平台：**Vercel**（不在 CF Pages、因為 Vercel 對 SPA 友善）
- 自動部署：push to `master` → 自動更新 Live Demo
- 預覽：dev branch 也會有 Preview URL

---

## 開發規範

- commit 訊息：繁體中文
- HTML 多版本歷史：舊版進 `archive/`、`index.html` 是 current
- 設計文件改動：硬約束（規格、API）進 `docs/`、軟敘述（世界觀、想法）進 `notes/`
- 重大架構決策寫進 `meetings/`（在 `matrix-manager/meetings/`）

---

## 相關文件

- MVP 規格：[`docs/ShadowProtocol_MVP_v0.1.md`](docs/ShadowProtocol_MVP_v0.1.md)
- 世界觀總覽：[`notes/Shadow_Protocol_世界觀與系統總覽.md`](notes/Shadow_Protocol_世界觀與系統總覽.md)
- 白皮書 v2：[`notes/Shadow_Protocol_Whitepaper_v2.0.md`](notes/Shadow_Protocol_Whitepaper_v2.0.md)
- LL 宇宙狀態：[`matrix-manager/UNIVERSE.md`](../matrix-manager/UNIVERSE.md)
