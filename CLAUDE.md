# CLAUDE.md — Shadow Protocol 專案背景

> 給 Claude 自己看的，用來快速重建上下文。

---

## 這個專案是什麼

**暗影協定 Shadow Protocol** — 一款同步回合制潛行策略遊戲，定位為教育用途（資安 × AI × 程式設計）。

隸屬於 **LeafLune 宇宙**「玄機界域 StrategySpace (SS)」品牌。

---

## 設計演化（重要背景）

早期版本叫 **ShadowPath 陰影之路**，是忍者主題的潛行遊戲。
後來改包裝成 **Shadow Protocol** 賽博龐克/資安風格，原因：
**為了教學現場**——「忍者暗殺」主題不適合校園，「資安攻防」則名正言順。
**玩法規則完全相同**，只是敘事框架不同。

ShadowPath 文件 = 內部設計底稿
Shadow Protocol 文件 = 對外正式版本

---

## 機制對照（忍者 → 資安）

| 原始概念 | 資安包裝 |
|----------|---------|
| 陰影隱身 | 加密通道（Encrypted Zone） |
| 光照暴露 | 開放通道（Open Channel） |
| 燭火/火把 | 掃描節點（Scan Node） |
| 聲音偵測 | 流量監測（Traffic Monitor） |
| 忍者刺殺 | 資料奪取/節點攻擊 |
| 守衛巡邏 | 防毒掃描（Antivirus Scan） |

---

## 核心機制摘要

- **同步回合制**：玩家與 AI 同時提交，同時結算
- **Sub-tick 系統**：依 speed 值切分小回合，支援不同速度物件共存
- **光影系統**：陰影格隱身，離開或攻擊即暴露
- **聽覺系統**：聲源半徑 × 聽覺半徑交集 = 被聽見；穿透牆壁但有衰減
- **控制模式**：直控 `:` / 指令 `>` / 腳本 `$`
- **可見性**：開燈 / 迷霧（EnemyVisible = Lit∧FOV 或 NV）/ 關燈（FOV 打洞）

---

## 四個角色模組

| 模組 | 特色 |
|------|------|
| 🥷 滲透程式 | 高機動、低噪音、高爆發；血少 |
| 👮 防毒程式 | 穩定耐久、掃描光錐、需休眠回能 |
| 👷 工作程式 | 無限能量、地形改造；無攻擊、感知極弱 |
| 🐕 偵測程式 | 最高速、夜視+聽覺最強；血少 |

---

## MVP 目標（v0.1）

- 10×10 格地圖、忍者、直控模式、開燈
- 物件：蠟燭 ×1、卷軸 ×1、出口 ×1；無敵人
- 操作：方向鍵移動、X 熄燭、O 撿卷軸
- 終端事件：move/blocked/extinguish/pick/exit/error
- 視覺：Konva 五層（grid / walls / items / actors / ui）

---

## 對戰模式（進階）

- **自走模式**：雙方全 Blockly 腳本，純演算法對抗
- **主帥模式**：人類 vs LLM 各控一名主帥，其餘單位腳本自動

---

## 長期生態願景

放置對戰 + 賞金池（BT）+ LLM 關主（Static→Adaptive→LLM Commander→Protocol Sentinel）+ 策略演化公開機制（連勝解鎖腳本公開）

---

## 檔案索引

| 檔案 | 內容 |
|------|------|
| `LL_Universe_MasterPlan_v1.md` | LeafLune 宇宙總藍圖 |
| `Shadow_Protocol_世界觀與系統總覽.md` | 世界觀、三陣營設定 |
| `💠 Cyber Protocol：暗影協定.md` | 四模組詳細數值表 |
| `ShadowPath_陰影之路.md` | 早期設計底稿（機制參考） |
| `ShadowProtocol_MVP_v0.1.md` | 最小可玩版規格 |
| `ShadowProtocol_Mode_Visibility_Spec.md` | 控制模式 × 可見性規格 |
| `ShadowProtocol_MirrorModes.md` | 自走模式 vs 主帥模式 |
| `ShadowProtocol_ProgramSystem.md` | 程式系統 × 資安轉譯 |
| `Shadow_Protocol_Whitepaper_v2.0.md` | 生態系白皮書 |
| `index.html` | 遊戲原型（半成品） |

---

## 注意事項

- **不要未確認就直接建檔或執行**，這個 owner 習慣先討論再動手
- ShadowPath 相關名詞（忍者、守衛、猎犬）= Shadow Protocol 對應角色，只是舊包裝
- 圖片 `cover.png` 是 Gemini 生成的封面圖
