
Impact of Biophysical & Neurological Constraints on Locomotion Learning
身体的・神経的制約がAIの歩行学習と進化に与える影響の検証
![alt text](https://img.shields.io/badge/Unity-2022.3+-black.svg?style=flat&logo=unity)

![alt text](https://img.shields.io/badge/ML--Agents-Release_21-blue.svg)

![alt text](https://img.shields.io/badge/Python-3.8+-yellow.svg?style=flat&logo=python)

![alt text](https://img.shields.io/badge/License-MIT-green.svg)
📖 Overview
本プロジェクトは、Unity ML-Agentsを用いた強化学習実験です。
ML-Agents-Developに内蔵されている標準的なエージェントに対し、「身体の巨大化に伴う筋力不足（2乗3乗の法則）」や「神経伝達速度の遅延（反応速度の低下）」といった生物学的な制約を与えた際、AIがどのような生存戦略（歩行フォーム）を独自に獲得するかを検証しました。
実験の結果、**「ハンディキャップを持つ個体は、標準個体とは異なる特化型の進化を遂げる」**という、人間の障害やニューロダイバーシティ（神経多様性）にも通じる示唆が得られました。
<!-- ここにデモ動画4つ。各モデルの歩行と全体像で計4 -->
<!-- ![Demo GIF](docs/demo.gif) -->
🎯 Motivation
強化学習エージェントは通常、理想的な身体と即時反応可能な神経系を持ちますが、現実の生物は物理的・生理的な制約下で運動を獲得します。
「もしAIに個体差（ハンディキャップ）があったらどうなるか？」という疑問から、以下の2つの仮説モデルを作成しました。
Scale Model (物理的制約: 2乗3乗の法則)
身長が伸びると体重は体積（3乗）で増えるが、筋力は断面積（2乗）でしか増えない。この「相対的な筋力低下」にどう適応するか？

Delayed Model (神経的制約: 認知遅延)
認知から行動までのプロセスを意図的に遅らせた場合、予測制御やバランス感覚はどう変化するか？

⚙️ Experiment Setup
1. Scale Model (Big Size)
身長を1.5倍に設定。生物物理学的な整合性を保つため、質量と筋力を以下の法則に従ってスケーリングしました。体重あたりの筋力（Power-to-Weight Ratio）は約66%に低下し、重力負荷が高い環境となります。
Parameter
Multiplier
Formula
Physics Reason
Height
x1.5
       LLL
     
Base scaling
Mass
x3.375
       L3L^3L3
     
体積は3乗で増加
Strength
x2.25
       L2L^2L2
     
筋力（断面積）は2乗で増加
2. Delayed Model (Latency)
身体能力は標準モデルと同一ですが、行動決定の頻度（Decision Period）を粗くすることで「情報処理の遅延」を再現しました。
Model
Decision Period
Simulation
Normal
10 frames
健常な反応速度
Delayed
20 frames
知覚-行動ループの遅延（約2倍の反応時間）
📊 Results & Analysis
1. 環境適応と報酬獲得 (Cumulative Reward)
![alt text](images/cumulative_reward.png)
Normal (水色): 安定した学習曲線を描く。
Scale (オレンジ): 筋力不足により初期学習は遅れるが、着実に成長する。
Delayed (紫色): 学習初期は最も苦戦するが、最終段階ではNormalやScaleを上回り、最も高い報酬スコアを記録した。
2. 生存時間と安定性 (Episode Length)
![alt text](images/episode_length.png)
Normal: 最も長く歩き続けられる（安定性が高い）。
Scale: Normalに次いで安定。転倒頻度は低い。
Delayed: 報酬は高いが、生存時間（Episode Length）は圧倒的に短い。
3. ロス推移 (Policy Loss)
![alt text](images/policy_loss.png)
各モデルとも学習に伴い収束しているが、Delayedモデルは変動が激しく、常にギリギリの制御を行っていることが示唆される。
🧠 Discussion: "特化的進化"の考察
実験データから、ハンディキャップに対するAIの興味深い適応戦略が観測されました。
🐢 Scale Model: "慎重な保守派"
体が重く筋力が相対的に弱いこのモデルは、**「ゆっくりと歩くが、あまり転ばない」**戦略を獲得しました。
エネルギー効率を重視し、重心を低く保つフォームは、巨体を持つ生物の理にかなった進化と言えます。
⚡ Delayed Model: "ハイリスク・ハイリターンな特化"
最も驚くべき結果を示したのが遅延モデルです。
現象: 「生存時間は短いが、獲得報酬は最も多い」。
戦略: 反応が遅れるため、一度バランスを崩すと立て直せず転倒します。そこでAIは、**「転ぶまでの短い時間の間に、猛スピードで前進して距離（報酬）を稼ぐ」**という極端な戦略を選びました。
考察:
これは、与えられた制約下で目的関数（報酬最大化）を達成するための**「特化的進化（Specialized Evolution）」です。
人間社会においても、ADHDなどの特性を持つ人が特定の分野で爆発的な集中力を発揮したり、視覚に障害がある人が聴覚を鋭敏に発達させたりするように、「ある機能の欠損が、別の機能の過剰な発達や独自の戦略を生む」**という現象を、AIが自律的にシミュレーションしたと言えます。
この結果は、AIエージェントにおける「個性」とは、パラメータのランダム性だけでなく、制約条件への適応プロセスから生まれる可能性を示唆しています。
## 🚀 Future Prospects (今後の展望)

本実験の結果は、単なる歩行シミュレーションにとどまらず、次世代のAI開発において以下の応用可能性を示唆しています。

### 1. Robustness for Physical Robots (実機ロボットの冗長性確保)
現実のロボットは、バッテリー消耗によるトルク低下（Scaleモデルの状況）や、通信環境悪化によるレイテンシ（Delayedモデルの状況）を避けて通れません。
本プロジェクトのアプローチを応用し、あらかじめ「制約条件下での生存戦略」を学習させておくことで、ハードウェアトラブル発生時にも即座に「安全歩行モード」や「緊急移動モード」へ適応できる、極めてロバストな制御システムの構築に貢献できます。

### 2. AI Neurodiversity (制約が生む多様な知能)
最も興味深い発見は、**「制約（ハンディキャップ）が、標準モデルにはない特化した能力を開花させた」**点です。
これは人間社会におけるニューロダイバーシティ（神経多様性）と同様、AIにおいても「画一的な高性能」を目指すのではなく、「異なる制約を持ったAIのチーム」を作ることで、単一モデルでは解決できない複雑な課題を突破できる可能性を示しています。
今後は、異なる制約を持つエージェント同士を協力させる「多様性アンサンブル学習」への発展を視野に入れています。
🛠️ Technical Stack
Engine: Unity 2022.3.x
ML Library: Unity ML-Agents Release 21
Algorithm: PPO (Proximal Policy Optimization)
Observation: Vector Observation + Ray Perception Sensor 3D
Action: Continuous Action Space (Joint Torques)
👨‍💻 Author
[kmtkzy1379]
