# Impact of Biophysical Scaling and Neurological Latency on Bipedal Locomotion Learning
<!-- プロジェクトのキャッチコピー: 物理的制約と神経学的制約がAIの学習に与える影響の検証 -->

![Unity](https://img.shields.io/badge/Unity-2022.3+-black.svg?style=flat&logo=unity)
![ML-Agents](https://img.shields.io/badge/ML--Agents-Release_21-blue.svg)
![License](https://img.shields.io/badge/License-MIT-green.svg)

## 📖 Overview
本プロジェクトは、Unity ML-Agents を用いて、生物学的な制約条件（身体サイズの変化に伴う物理法則、および神経伝達速度の遅延）が、二足歩行エージェントの強化学習プロセスとその収束性にどのような影響を与えるかを検証した比較実験です。

「Square-Cube Law（2乗3乗の法則）」に基づく筋力不足モデルと、認知科学研究に基づく「情報処理遅延」モデルを作成し、標準モデル（Normal）との学習挙動の差異を分析しました。

<!-- ここにデモGIFを貼ると非常に効果的です -->
<!-- ![Demo GIF](docs/demo.gif) -->

## 🎯 Motivation & Hypothesis
強化学習エージェントは通常、理想的な身体と即時反応可能な神経系を持ちますが、現実の生物は物理的・生理的な制約下で運動を獲得します。本実験では以下の2つの仮説を検証しました。

1.  **Scale Model (Biophysical Constraint):**
    身長が大きくなると、体重は体積（3乗）で増加するのに対し、筋力は断面積（2乗）でしか増加しない（2乗3乗の法則）。この「相対的な筋力低下」という物理的制約下でも、エージェントは適応的な歩行を獲得できるか？
2.  **Delayed Model (Neurological Constraint):**
    加齢や障害による情報処理速度の低下（反応時間の遅延）は、FEP（自由エネルギー原理）における予測誤差の最小化ループを阻害すると考えられる。意図的に知覚-行動ループを遅延させた場合、学習の収束性や歩行フォームはどう変化するか？

## ⚙️ Experiment Setup

### 1. Scale Model (Square-Cube Law)
身長を1.5倍にした際、生物物理学的な整合性を保つため、質量と筋力を以下の法則に従ってスケーリングしました。結果として、**体重あたりの筋力（Power-to-Weight Ratio）は約66%に低下**し、より高負荷な環境となります。

| Parameter | Multiplier | Formula | Reason |
| :--- | :--- | :--- | :--- |
| **Height (Scale)** | **x1.5** | $L$ | Base scaling factor |
| **Mass (Weight)** | **x3.375** | $L^3$ | Volume increases by cube |
| **Strength (Torque)** | **x2.25** | $L^2$ | Muscle cross-section increases by square |
| **Vision (Ray)** | **x1.5** | $L$ | Adjusted to eye height |

### 2. Delayed Model (Reaction Time)
身体能力は標準モデルと同一のまま、純粋な「情報処理の遅延」を再現しました。
遅延倍率（2倍）の根拠として、高齢者や知的障害を持つ集団の反応時間が、健常者と比較して約1.5倍〜3倍（選択反応時）に遅延するという研究結果[*1][*2]を参照しました。

| Parameter | Normal Model | Delayed Model | Note |
| :--- | :--- | :--- | :--- |
| **Decision Period** | 10 frames | **20 frames** | Simulates 2x cognitive latency |
| **Implication** | - | - | Increases latency in the sensorimotor loop |

> **Reference:**
> *   [*1] Studies indicate that reaction times in elderly populations (70+) are approx. 1.5x (simple) to 3.0x (choice) slower compared to young adults.
> *   [*2] Research on intellectual disabilities suggests a 2x-3x delay in reaction times for complex motor tasks due to information processing speed.

## 📊 Results (検証結果)

<!-- ここに教えていただいた「結果」を記述します。以下はプレースホルダーです -->

### Learning Convergence (学習曲線)
*   **Scale Model:** 筋力対重量比の低下により、初期段階での学習効率は著しく低下しました。しかし、xx万ステップ付近で……（どのような適応を見せたか記述）。
*   **Delayed Model:** 決定周期の粗さ（20フレームごとの行動決定）により、フィードバック制御が間に合わず……（振動した、転倒しやすかった等の結果）。

<!-- TensorBoardの画像を貼る場所 -->
<!-- ![Training Graph](docs/training_graph.png) -->

### Gait Analysis (歩行分析)
*   **Normal:** 安定した走行。
*   **Scale:** （例：ストライドを短くし、重心を低く保つような歩行を獲得した）。
*   **Delayed:** （例：急な姿勢制御ができず、ゆっくりとした歩行に収束した）。

## 🛠️ Technical Stack
*   **Engine:** Unity 2022.3.x
*   **ML Toolkit:** Unity ML-Agents Release 21
*   **Algorithm:** PPO (Proximal Policy Optimization)
*   **Space:** Continuous Action Space / Vector Observation + Ray Perception

## 🧠 Discussion
（ここにFEPの観点などを絡めた考察を書きます。結果をいただければ肉付けします）
遅延モデルにおけるパフォーマンスの低下は、予測誤差（Prediction Error）のフィードバックが遅れることで、自己受容感覚（Proprioception）と実際の身体状態の解離が生じたためと考えられる……

## 👨‍💻 Author
[Your Name/Account]
