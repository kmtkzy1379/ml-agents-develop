# Impact of Biophysical & Neurological Constraints on Locomotion Learning
**身体的・神経的制約がAIの歩行学習と進化に与える影響の検証**

[![Unity Editor](https://img.shields.io/badge/Unity-6000.3.2f1-black.svg?style=flat&logo=unity)](Project/ProjectSettings/ProjectVersion.txt)
[![ML‑Agents (package)](https://img.shields.io/badge/com.unity.ml--agents-4.0.0-blue.svg)](com.unity.ml-agents/package.json)
[![Python (repo)](https://img.shields.io/badge/mlagents-1.2.0.dev0-yellow.svg)](ml-agents/mlagents/trainers/__init__.py)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

## 概要 / Overview
本プロジェクトは **Unity ML-Agents** をベースにした強化学習実験リポジトリです。

主な研究テーマは、**「身体的・神経的制約（サイズスケーリングによる筋力比低下、認知・神経遅延）が動的制御学習（歩行）に与える影響」** の調査です。物理的なハンディキャップや神経伝達の遅延が、エージェントの学習戦略や進化にどのような変化をもたらすかを検証します。

---

## 環境・要件 / Requirements
本リポジトリは以下の環境で構成されています。プロジェクトを開く際は、Unity Editorのバージョンにご注意ください。

### Unity Environment
- **Unity Editor**: `6000.3.2f1` (Unity 6)
- **ML-Agents Package (C#)**: `4.0.0`

### Python Environment
- **Python**: `3.10` (推奨)
- **ML-Agents (Python)**: `1.2.0.dev0` (Development Build)
- **ML-Agents Envs**: `1.2.0.dev0`

---

## インストール / Installation

リポジトリをクローンし、UnityプロジェクトとPython仮想環境のセットアップを行います。

### 1. クローン
```bash
git clone https://github.com/kmtkzy1379/ml-agents-develop.git
cd ml-agents-develop
```
2. Unity プロジェクトのセットアップ

Unity Hub を起動し、Add からクローンしたディレクトリ内の Project/ フォルダを選択してリストに追加します。

Unity Editor バージョン 6000.3.2f1 でプロジェクトを開きます。

※ 初回起動時はパッケージの解決に時間がかかる場合があります。

3. Python 環境の構築

Python 3.10 の仮想環境を作成し、リポジトリに含まれる開発版パッケージをインストールします。

```bash
# 仮想環境の作成と有効化
python3.10 -m venv .venv
source .venv/bin/activate   # Windows (PowerShell): .venv\Scripts\activate

# 基本ツールのアップグレード
pip install -U pip setuptools wheel

# ML-Agents パッケージのインストール（Editable Install）
pip install -e ./ml-agents-envs
pip install -e ./ml-agents
```
Note: PyTorchなどの依存ライブラリは、お使いの環境（CUDAバージョン等）に合わせて適切にインストールしてください。

使い方 / Usage
トレーニングの実行

Unity Editor で学習させたいシーンを開きます。

エージェントの Behavior Parameters（Continuous Actions, Ray Perception Sensor 等）が正しく設定されていることを確認します。

ターミナルで以下のコマンドを実行し、Unity Editor 側で Play ボタンを押します。

```bash
# 基本的な学習コマンド
mlagents-learn config/your_config.yaml --run-id=run01 --train
```
※ config/ ディレクトリ内の yaml ファイルや、--run-id は実験に合わせて変更してください。

実験内容 / Experiments

本プロジェクトでは、標準モデルに対して2つの制約モデルを作成し、学習結果を比較しています。

比較モデル

Scale Model (物理的制約)

身長を1.5倍、体重を体積則に従い増加させたモデル。

筋力は断面積則でスケールするため、体重に対する相対的な筋力が低下している状態。

Delayed Model (神経的制約)

Decision Period（意思決定の間隔）を粗く設定し、反応遅延（神経伝達の遅れ）を再現したモデル。

結果の傾向

Scale Model: ゆっくりだが安定した歩行を行う「保守的戦略」を獲得。

Delayed Model: 高い報酬を得ることもあるが転倒しやすい「ハイリスク・ハイリターン」な動作に特化。

これらの結果から、制約条件下における「特化的適応（Specialized Evolution）」についての考察を行っています。


License

MIT License

Author

kmtkzy1379

code
Code
download
content_copy
expand_less
