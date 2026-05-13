# TODO.md — Shadow Protocol

---

## ⬡ MM 同步

| title | status | importance | energy | effort | due | next_action | tags |
|-------|--------|------------|--------|--------|-----|-------------|------|
| 觀戰 UI（既有等待中項目）| queued | 2 | m | 240 | | 等 MVP 主體穩定再上 | SP,ui |
| Agentic Curriculum Phase 0 PoC | idea | 2 | h | 480 | | 純 Python Generator + Tester 跑 100 關 | SP,curriculum,research |
| Agentic Curriculum Phase 1 整合 | idea | 2 | h | 720 | | Generator 輸出整合進 SP MVP | SP,curriculum,integration |
| MVP v0.1 收尾 | active | 2 | m | 360 | | 直控模式六類事件完整測試 | SP,mvp |
| 文件治理整理（已完成）| done | 2 | l | 60 | | — | SP,governance |

---

## MVP v0.1 收尾（既有）

- [ ] 直控模式六類事件完整實作 + 終端輸出對齊
  > 詳見 `docs/ShadowProtocol_MVP_v0.1.md` Section 2
- [ ] 視覺層 Konva 結構驗收（gridLayer / wallsLayer / itemsLayer / actorsLayer）
- [ ] 10×10 網格邊界處理（牆 / 越界判斷）
- [ ] 蠟燭 / 卷軸 / 出口物件互動測試
- [ ] Live Demo 部署驗證（Vercel）

---

## 觀戰 UI（等 MVP 主體完成）

- [ ] 觀戰模式設計（讓非玩家看別人玩）
- [ ] 跟 SS 平台對接（如果未來要做天梯 / 排位）
- [ ] UI 完成後、SP 從「等觀戰 UI 才上」狀態畢業

---

## Agentic Curriculum（新方向、2026-05-13 規劃）

> 詳細 framing 見 `PROJECT.md` 末段「演進方向」

### Phase 0：PoC（最小驗證、1 週）

- [ ] 寫 Generator（純 Python）
  > 輸入：難度參數（牆密度 / 燭數 / 最短路徑長 / 分支因子）
  > 輸出：10×10 關卡 JSON（牆 / 燭 / 卷 / 出口 / spawn）
- [ ] 寫 Tester（純 Python）
  > BFS / A* 求最短解、計算難度分數
- [ ] 跑 100 次、輸出難度分布圖（histogram）
- [ ] 人工 review 10 個關卡、確認 Tester 評分合理
- [ ] 確認 Generator 能 detect「無解關卡」（要能讓 Tester 篩掉）

### Phase 1：整合進 SP MVP（2 週）

- [ ] Generator 輸出對齊 SP 既有關卡 JSON 格式
- [ ] 把 100 關按難度排序、塞進 SP Chapter 1-3
- [ ] Tester 算出的最短解、給玩家當 hint（提示「最少 X 步可解」）
- [ ] SP UI 加「難度顯示」（★★★★★）
- [ ] 體感驗證：玩 5 關、看體感難度跟 Tester 評分一致嗎
- [ ] 不一致 → 調 Tester 難度公式

### Phase 2：對抗式迭代（可選、後期）

- [ ] 設計「無聊關卡 / 太難關卡」penalty
- [ ] Generator 根據 reward 調參
- [ ] 接近 GAN 結構、但 ROI 後期評估

---

## 已完成

- [x] MVP v0.1 規格初稿（`docs/ShadowProtocol_MVP_v0.1.md`）
- [x] 世界觀文件、白皮書 v2、控制模式規格等設計文件
- [x] Live Demo 部署 Vercel
- [x] 文件治理整理：建 docs/ notes/ archive/、CLAUDE.md 從 MM 複製、新建 PROJECT.md + TODO.md（2026-05-13）

---

## 擱置

- 多人連線（同步回合制、複雜度高）
  > 擱置原因：MVP 還沒完、單機優先

- 「Cyber Protocol：暗影協定」品牌分支
  > 擱置原因：notes/ 內有相關文件、但目前以 Shadow Protocol 為主名稱
