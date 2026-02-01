# 🦴 智脊 Smart Spine - 您的智慧坐姿健康管家

> 「讓智脊，成為你人生中的知己。」
> **智脊 (Smart Spine)** 是一款基於電腦視覺的即時坐姿監測系統，旨在解決現代人長期久坐導致的脊椎健康問題。本專案發源於 **清大立德 AI 冬季實戰工作坊**，實現了從數據採集、特徵工程到模型部署的全棧開發流程。


---

## 專案參與人
Frey 傅暐程 frey.50302.fu.123@gmail.com
刁元廷 tjimmy0113@gmail.com
Alvin ooii8929@gmail.com

---

## 💡 專案 Demo
https://youtu.be/kE5gtMvK_TI
https://drive.google.com/file/d/11X3Vzp-c48s-IwMnMFBf-W5gu10aM6xj/view?usp=sharing

---

## 💡 專案亮點

* **端點偵測技術**：採用 **PoseNet** 進行 17 個關鍵點偵測，並針對特定場景優化。
* **高維特徵工程**：將關鍵點座標與影像區域特徵融合，展開成 **14,739 維** 的特徵向量，捕捉細微的姿勢差異。
* **輕量化部署**：透過 Web 技術實現，無需安裝環境，開啟瀏覽器即可進行推論，極大化使用者體驗。

---

## 🛠 技術架構

### 系統分析工作流

本系統透過分析人體上半身核心節點，精準判斷受試者是否處於「正確坐姿」或「錯誤姿勢」。

| 階段 | 說明 |
| --- | --- |
| **影像輸入** | 透過 WebCam 或圖片進行即時串流輸入。 |
| **關鍵點偵測** | 使用 **PoseNet** 提取 17 個身體關鍵點（包含五官、雙肩、雙肘、雙髖等）。 |
| **特徵展平** | 提取關鍵點座標與局部影像特徵，融合為 **14,739 維特徵向量**。 |
| **分類推論** | 傳入自定義的神經網絡分類器進行二分類（Binary Classification）。 |
| **結果輸出** | 即時反饋正確/錯誤機率，並提醒使用者調整姿勢。 |

---

## 🧠 模型設計 (Model Architecture)

為了在網頁端保持高效能與準確率，我們設計了一個精簡而強大的 MLP（多層感知器）：

* **Input Layer**: 14,739 Features
* **Dense Layer 1**: 100 Neurons (ReLU activation)
* **Regularization**: Dropout (50%) - *有效防止過擬合，提升泛化能力。*
* **Output Layer**: 2 Neurons (Softmax activation) - *輸出正確與錯誤坐姿的機率分布。*

---

## 📊 關鍵點定義 (17 Keypoints)

系統監控的 17 個核心端點如下：

| ID | 部位 | ID | 部位 |
| --- | --- | --- | --- |
| 0 | 鼻子 | 9-10 | 左右手腕 |
| 1-2 | 左右眼 | 11-12 | 左右臀部 |
| 3-4 | 左右耳 | 13-14 | 左右膝蓋 |
| 5-6 | 左右肩膀 | 15-16 | 左右腳踝 |
| 7-8 | 左右手肘 |  |  |

---

## 🚀 快速上手 (Quick Start)

本專案採用 Web 技術開發，支援即啟即用：

1. **複製儲存庫**
```bash
git clone https://github.com/your-username/smart-spine.git
cd smart-spine
```


2. **啟動本地伺服器** (推薦使用 Python)
```bash
python -m http.server 8000

```


3. **執行應用**
在瀏覽器開啟 `http://localhost:8000/posture_detection.html`

---

## 📁 檔案說明

* `posture_detection.html`: 核心應用程式，整合 PoseNet 與 Teachable Machine 推論引擎。
* `posture_detection_architecture.docx`: 詳細的技術規格說明與產品規劃書。
* `README.md`: 專案概覽與開發文檔。

---

## 🤝 參考資料

* **Dataset Source**: [Human Pose Dataset](https://dayta.nwu.ac.za/articles/dataset/Human_pose_dataset_sit_stand_pose_classes_/23290937)
* **Training Platform**: [Teachable Machine](https://teachablemachine.withgoogle.com/train)
* **Technical Reference**: [Building Pose Analysis System (OpenCV)](https://learnopencv.com/building-a-body-posture-analysis-system-using-mediapipe/)
