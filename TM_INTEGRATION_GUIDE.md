# 使用你的 Teachable Machine 模型 - 完整指南

## 📁 檔案結構

你需要以下檔案結構：

```
你的資料夾/
├── posture_detection_tm.html  (主程式)
└── tm_model/                  (模型資料夾)
    ├── model.json
    ├── metadata.json
    └── weights.bin
```

## 🚀 快速開始（三種方法）

### 方法 1：使用 Python 本地伺服器（最簡單）

1. **放置檔案**
   ```
   將 posture_detection_tm.html 和 tm_model 資料夾放在同一目錄
   ```

2. **啟動伺服器**
   ```bash
   # 在檔案所在目錄開啟終端機
   python -m http.server 8000
   
   # 或者如果是 Python 2
   python -m SimpleHTTPServer 8000
   ```

3. **開啟瀏覽器**
   ```
   http://localhost:8000/posture_detection_tm.html
   ```

### 方法 2：使用 Node.js

1. **安裝 http-server**
   ```bash
   npm install -g http-server
   ```

2. **啟動伺服器**
   ```bash
   http-server -p 8000
   ```

3. **開啟瀏覽器**
   ```
   http://localhost:8000/posture_detection_tm.html
   ```

### 方法 3：上傳到網路空間（最方便）

1. **上傳檔案**
   - 將所有檔案上傳到 GitHub Pages、Netlify、或任何網頁空間
   
2. **直接訪問**
   - 例如：https://yourusername.github.io/posture-detection/

---

## 🔧 如果遇到 CORS 錯誤

### 問題症狀
```
Access to fetch at 'file:///...' has been blocked by CORS policy
```

### 解決方法

#### A. 修改 HTML（如果模型在線上）

如果你的模型上傳到網路空間：

```javascript
// 在 HTML 的 <script> 中找到這行：
const MODEL_URL = "./tm_model/";

// 改成你的網路位置：
const MODEL_URL = "https://yourserver.com/path/to/tm_model/";
```

#### B. 使用本地伺服器（推薦）

永遠使用 `python -m http.server` 或類似工具，不要直接雙擊 HTML 開啟。

---

## 📊 關於你的模型

### 模型資訊
- **訓練平台**: Teachable Machine Pose
- **模型架構**: MobileNetV1
- **類別數量**: 2 類
  - 類別 0: "正確的"
  - 類別 1: "錯誤的"
- **訓練樣本**: 各 7 張（總共 14 張）

### 為什麼準確度可能不理想？

#### 1. **訓練資料太少**
```
目前: 7 張正確 + 7 張錯誤 = 14 張

建議:
- 正確姿勢: 50-100 張
- 錯誤姿勢: 100-200 張
  - 駝背: 50 張
  - 前傾: 50 張
  - 歪斜: 50 張
  - 其他: 50 張
```

#### 2. **資料多樣性不足**
你的 7 張照片可能：
- 同一個人
- 相同背景
- 相同光線
- 相同衣服
- 相同角度

**改善方法：**
- 不同人（不同體型、身高）
- 不同環境（家裡、辦公室、咖啡廳）
- 不同光線（明亮、昏暗、自然光、燈光）
- 不同衣服（深色、淺色、圖案）
- 不同距離（近、中、遠）
- 不同角度（正面、稍微側面）

#### 3. **Teachable Machine Pose 的限制**

Teachable Machine Pose 實際上是：
```
你的照片 → PoseNet 偵測關鍵點 → 分類器 → 結果
```

問題：
- 它會學到照片的背景、顏色等無關特徵
- 需要大量資料才能準確

---

## 🎯 改善模型準確度的步驟

### Step 1: 重新收集資料（使用我的工具）

1. **開啟 data_collector.html**
   - 這個工具會幫你收集 MediaPipe 關鍵點資料

2. **收集正確姿勢**
   - 坐好標準姿勢
   - 按 C 鍵連續收集 100 次
   - 稍微改變角度、位置再收集
   
3. **收集錯誤姿勢**
   - 駝背: 按 X 鍵收集 50 次
   - 前傾: 按 X 鍵收集 50 次
   - 歪斜: 按 X 鍵收集 50 次
   - 低頭: 按 X 鍵收集 50 次

4. **下載資料**
   - 按 D 鍵下載 CSV 和 JSON

### Step 2: 重新訓練模型

#### 選項 A: 在 Teachable Machine 重新訓練

1. 回到 https://teachablemachine.withgoogle.com/train/pose
2. 上傳更多樣本（每類至少 50 張）
3. 確保多樣性：
   - ✅ 不同人
   - ✅ 不同背景
   - ✅ 不同光線
   - ✅ 不同衣服
4. 訓練並匯出新模型
5. 替換 tm_model 資料夾中的檔案

#### 選項 B: 使用我的工具訓練（更好）

我可以為你創建一個：
- 使用 MediaPipe 關鍵點的訓練工具
- 不受背景影響
- 需要較少資料
- 準確度更高

---

## 💡 測試你的模型

### 測試檢查清單

1. **基本功能測試**
   - [ ] 網頁能正常載入
   - [ ] 攝影機能正常啟動
   - [ ] 能看到骨架繪製
   - [ ] 信心度條有反應

2. **準確度測試**
   - [ ] 坐好標準姿勢 → 應該顯示「正確的」（信心度 >70%）
   - [ ] 駝背 → 應該顯示「錯誤的」（信心度 >70%）
   - [ ] 前傾 → 應該顯示「錯誤的」
   - [ ] 歪斜 → 應該顯示「錯誤的」

3. **穩定性測試**
   - [ ] 保持同一姿勢，判斷不會頻繁跳動
   - [ ] 改變光線，判斷不受影響
   - [ ] 改變背景，判斷不受影響

### 如果測試失敗

**情況 1: 隨機判斷（信心度都在 50% 左右）**
→ 模型沒有學到東西，需要重新訓練

**情況 2: 總是判斷錯誤**
→ 可能標籤顛倒了，或者訓練資料有問題

**情況 3: 信心度很低（<60%）**
→ 模型不確定，需要更多訓練資料

**情況 4: 頻繁跳動**
→ 模型不穩定，需要更多訓練資料

---

## 🔬 調試技巧

### 1. 查看瀏覽器 Console

按 F12 開啟開發者工具，查看：
```javascript
// 應該看到：
模型載入成功！類別數量: 2

// 如果看到錯誤：
Failed to fetch
// → 檔案路徑不對或 CORS 問題

Cannot read property 'className' of undefined
// → 模型結構有問題
```

### 2. 檢查模型檔案

確認三個檔案都存在且完整：
```bash
ls -lh tm_model/
# 應該看到：
# model.json (約 1-5 KB)
# metadata.json (約 1 KB)
# weights.bin (約 1-10 MB)
```

### 3. 測試模型載入

在 Console 輸入：
```javascript
fetch('./tm_model/model.json')
  .then(r => r.json())
  .then(d => console.log(d))
```

如果成功，會顯示模型結構。

---

## 🎓 進階優化

### 1. 增加信心度閾值

如果模型經常誤判，可以設定最低信心度：

在 HTML 中的 `updatePrediction` 函數中加入：

```javascript
// 只有當信心度超過 70% 才判定
if (maxConfidence < 0.7) {
    // 信心度不足，不更新判斷
    return;
}
```

### 2. 平滑判斷結果

避免頻繁跳動：

```javascript
// 在全域變數加入
let recentPredictions = [];
const BUFFER_SIZE = 5;

// 在 updatePrediction 中
recentPredictions.push(isCorrect);
if (recentPredictions.length > BUFFER_SIZE) {
    recentPredictions.shift();
}

// 使用多數投票
const correctCount = recentPredictions.filter(x => x).length;
const finalDecision = correctCount > BUFFER_SIZE / 2;
```

### 3. 混合使用規則判斷

結合 MediaPipe 關鍵點的規則判斷：

```javascript
// 如果 AI 不確定（信心度 <70%），使用規則判斷
if (maxConfidence < 0.7) {
    // 使用之前的角度計算方法
    const shoulderAngle = calculateShoulderAngle(pose);
    // ...
}
```

---

## 📞 常見問題

### Q1: 為什麼顯示 "載入失敗"？

**A:** 可能原因：
1. 沒有使用本地伺服器 → 用 `python -m http.server`
2. 模型檔案路徑不對 → 檢查 `tm_model` 資料夾位置
3. 模型檔案損壞 → 重新從 Teachable Machine 匯出

### Q2: 為什麼總是判斷錯誤？

**A:** 
1. 訓練資料太少（只有 7 張）
2. 訓練資料不夠多樣
3. 可能學到了背景而不是姿勢

**解決：** 用 data_collector.html 收集 300+ 張，或回 Teachable Machine 重新訓練

### Q3: 可以在手機上使用嗎？

**A:** 可以！但需要：
1. 上傳到網路空間（不能用 file://）
2. 使用 HTTPS（安全連線）
3. 手機效能要夠好

### Q4: 如何匯出更好的模型？

**A:** 在 Teachable Machine：
1. 增加訓練樣本到 50+ 張每類
2. 確保樣本多樣性
3. 訓練時增加 Epochs（訓練次數）
4. 使用 "Advanced" 設定

---

## 🎁 我可以提供的額外工具

1. **模型品質分析器** - 告訴你模型哪裡需要改進
2. **自動資料增強器** - 從少量照片生成更多訓練資料
3. **混合判斷系統** - AI + 規則判斷，準確度更高
4. **模型訓練工具** - 在網頁中直接訓練，不用 Teachable Machine

需要的話告訴我！

---

## 📚 相關資源

- Teachable Machine: https://teachablemachine.withgoogle.com/
- TensorFlow.js: https://www.tensorflow.org/js
- MediaPipe Pose: https://google.github.io/mediapipe/solutions/pose

---

**總結：** 你的模型只有 7+7 張訓練資料，這太少了！建議至少收集 50+50 張，並確保多樣性。使用我提供的 data_collector.html 可以更有效率地收集資料。
