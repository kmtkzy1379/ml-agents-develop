# Impact of Biophysical & Neurological Constraints on Locomotion Learning

**身体的・神経的制約がAIの歩行学習に与える影響**

![Unity](https://img.shields.io/badge/Unity-6000.3.2f1-black.svg?logo=unity)
![ML-Agents](https://img.shields.io/badge/com.unity.ml--agents-4.0.0-blue.svg)
![Python](https://img.shields.io/badge/mlagents-1.2.0.dev0-yellow.svg)
![License](https://img.shields.io/badge/License-MIT-green.svg)

---

## 概要 / Overview

本リポジトリは **Unity ML-Agents** を用いた強化学習実験プロジェクトです。

研究目的は、

> **身体的制約（スケール変化による筋力比低下）** および
> **神経的制約（意思決定・反応の遅延）**

が、**二足歩行の学習戦略や運動様式にどのような影響を与えるか** を検証することです。

---

## 研究背景 / Motivation

実世界の生物は、

* 体格差による力学的不利
* 神経伝達や認知処理の遅延

といった制約の中で運動を最適化しています。

本研究ではこれらを **人工エージェントに明示的に課す** ことで、
制約下で生じる **戦略の変化・特化的適応（Specialized Evolution）** を観察します。

---

## 環境 / Requirements

### Unity

* **Unity Editor**: `6000.3.2f1` (Unity 6)
* **ML-Agents (C#)**: `4.0.0`

### Python

* **Python**: `3.10`（推奨）
* **ml-agents**: `1.2.0.dev0`
* **ml-agents-envs**: `1.2.0.dev0`

> ⚠️ PyTorch は CUDA 環境に応じて別途インストールしてください。

---

## セットアップ / Installation

### 1. リポジトリの取得

```bash
git clone https://github.com/kmtkzy1379/ml-agents-develop.git
cd ml-agents-develop
```

### 2. Unity プロジェクト

1. Unity Hub → **Add**
2. `Project/` フォルダを指定
3. Unity `6000.3.2f1` で起動

※ 初回起動時はパッケージ解決に時間がかかります。

### 3. Python 環境

```bash
python3.10 -m venv .venv
source .venv/bin/activate  # Windows: .venv\\Scripts\\activate

pip install -U pip setuptools wheel
pip install -e ./ml-agents-envs
pip install -e ./ml-agents
```

---

## 使い方 / Usage

1. Unity Editor で学習用シーンを開く
2. **Behavior Parameters** が正しく設定されていることを確認
3. ターミナルで以下を実行

```bash
mlagents-learn config/your_config.yaml --run-id=run01 --train
```

4. Unity Editor で ▶ **Play**

---

## 実験設計 / Experiments

### 比較モデル

#### 1. Baseline Model

* 標準的な体格・反応速度

#### 2. Scale Model（身体的制約）

* 身長: **1.5倍**
* 質量: **体積則に従い増加**
* 筋力: **断面積則スケーリング** → 相対筋力低下

#### 3. Delayed Model（神経的制約）

* Decision Period を増加
* 意思決定・反応遅延を再現

---

## 観察された傾向 / Results

| モデル           | 獲得された戦略       |
| ------------- | ------------- |
| Scale Model   | 低速・安定志向の保守的歩行 |
| Delayed Model | 転倒リスクの高い高報酬行動 |

これらは **制約に対する異なる最適解** が存在することを示唆します。

---

## 考察 / Discussion

* 制約は単なる性能低下ではなく **戦略空間の再構成** を引き起こす
* 神経遅延は「慎重さ」ではなく「投機性」を誘発する場合がある
* 身体制約は運動の安定性を優先する方向へ適応を促す

---

## License

MIT License

---

## Author

**kmtkzy1379**
