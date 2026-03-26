
# Shadow Protocol — 最小 MVP 規劃（v0.1）

> 目標：在**直控 × 開燈**環境下，玩家能移動、熄燭、撿卷、抵達出口通關；終端能明確回饋事件。

---

## 1) 範圍（只做這些）
- **章節/主角**：忍者（Chapter 1）  
- **控制模式**：直控（提示符 `:`）  
- **可見性**：開燈（暗幕關閉）  
- **地圖**：10×10 網格（`cellSize` 可調），邊界視為牆  
- **物件**：牆、蠟燭 ×1、卷軸 ×1、出口 ×1  
- **敵人**：此版不做（0 敵方 AI）  
- **操作**：
  - `↑ ↓ ← →`：移動一格（不可穿牆/越界）
  - `X`：熄滅**正前方一格**的蠟燭（若存在）
  - `O`：撿起**腳下**的卷軸（若存在）

---

## 2) 終端（必要事件與格式）
提示符（直控）：`:`  
建議行為→結果的單行格式：`:<action> | <result>`

必要事件型別：
- `: move up | ok`
- `: move right | blocked_wall`
- `: extinguish | candle_off`
- `: pick | picked_scroll`
- `: exit | success`
- `: error | out_of_bounds`

> 先確保這 6 類事件完整打印；顏色/圖示後續再加。

---

## 3) 視覺層（Konva 最小結構）
- `gridLayer`：格線
- `wallsLayer`：牆
- `itemsLayer`：蠟燭（亮/滅狀態）、卷軸、出口
- `actorsLayer`：玩家（忍者）
- `uiLayer`（可選）：游標框／高亮

> **開燈**：不建立暗幕層，省實作成本。

---

## 4) 狀態模型（最小）
```txt
GameState {
  grid: { cols, rows, cellSize },
  player: { x, y, dir },         // dir: N/E/S/W
  items: {
    candles: [{ x, y, isOn }],
    scroll: { x, y, isPicked },
    exit:   { x, y }
  },
  walls: Set<"x,y">,
  log: string[]                   // 終端列印文本
}
```

---

## 5) 地圖檔（JSON 範本）
```json
{
  "cols": 10,
  "rows": 10,
  "cellSize": 48,
  "player": { "x": 1, "y": 1, "dir": "E" },
  "walls": ["3,1", "3,2", "3,3", "3,4"],
  "candles": [{ "x": 5, "y": 2, "isOn": true }],
  "scroll": { "x": 7, "y": 4 },
  "exit":   { "x": 1, "y": 8 }
}
```

---

## 6) 規則重點
- **移動**：一次一格；牆/越界 → `blocked_wall` / `out_of_bounds`
- **熄燭**：面朝方向的鄰格有蠟燭且 `isOn=true` → `candle_off` 並改狀態
- **撿卷**：玩家站在卷軸座標 → `picked_scroll` 並隱藏卷軸
- **通關**：已撿卷，玩家站在出口座標 → `success` 並鎖輸入（顯示「按 R 重來」）
- **可調**：`cellSize` 可改，繪製與命中應一致更新

---

## 7) 驗收清單（打勾即通過）
- [ ] 直控可移動，牆體/越界判定正確並打印結果  
- [ ] 可熄滅前方一格的蠟燭並打印 `candle_off`  
- [ ] 可撿起卷軸並打印 `picked_scroll`  
- [ ] 抵達出口後打印 `success` 並鎖輸入  
- [ ] `cellSize` 變更後，格線與碰撞仍正確  
- [ ] 終端覆蓋上述 6 類事件

---

## 8) 之後的增量路線（僅列順序，不在 v0.1 實作）
1. **v0.2**：指令模式（仍開燈）— N=4 佇列、逐步執行、終端 `[i/N]` 回饋  
2. **v0.3**：指令 × 迷霧 — 套用迷霧規則與簡易風險預視（Lit/FOV/NV 標記）  
3. **v0.4**：腳本 × 關燈 — 腳本僅用 FOV 內資訊，UI 以 FOV 打洞；通關回放可開燈

---

## 9) 命名與常數（先釘住對齊文件與代碼）
- 模式：`MODE_DIRECT / MODE_COMMAND / MODE_SCRIPT`
- 可見性：`VIS_BRIGHT / VIS_FOG / VIS_DARK`
- 指令步數（未來用）：`CMD_STEPS = 4`
- 終端提示符：直控 `:`、指令 `>`、腳本 `$`

---

**備忘**：MVP 只求「能玩、能過、能印 log」。美術、特效、敵人、迷霧與腳本全部留到 v0.2+。
