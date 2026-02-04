# BEIG PoC - Adaptive Decision Making Framework

[![Python 3.11+](https://img.shields.io/badge/Python-3.11%2B-blue)](https://www.python.org/downloads/)

Proof of Concept for applying Bayesian belief updating and information theory to various decision-making scenarios through Claude Code plugins.

## Overview

このプロジェクトは、[symbiosis](https://github.com/h315uk3/symbiosis)リポジトリのwith-meプラグインの理論を検証し、様々なユースケースに適用するPoCです。

基本的なメカニズムは共通：
- **Adaptive Questioning** - Expected Information Gain (EIG)を最大化する質問生成
- **Bayesian Belief Updating** - 回答に基づく信念の更新
- **Entropy-Based Convergence** - 不確実性の測定と収束検出
- **5次元フレームワーク** - 各ユースケースに合わせた5つの要件次元
- **Local-First** - 全データをローカルに保存、外部サービス不要

## Plugins

### 1. with-me (Software Requirements)

ソフトウェア開発における要件抽出を支援するプラグイン。

**5次元**:
- Purpose - 解決する問題と対象ユーザー
- Data - 入出力データと変換
- Behavior - 操作フローと動作
- Constraints - 技術的制約と性能要件
- Quality - 成功基準とテスト戦略

**使用例**: 不明確な開発要件を体系的に明確化

### 2. lunch-decision (Lunch Choice)

ランチ選択を支援する適応的意思決定アシスタント。

**5次元**:
- Mood & Context - 気分と状況
- Taste Preferences - 味の好みと料理ジャンル
- Constraints - 予算、時間、場所の制約
- Health - 栄養目標と食事制限
- Decision Criteria - 決定の優先順位

**使用例**: 「今日のランチ何食べよう？」という日常的な意思決定

## Project Structure

```
.
├── .claude-plugin/          # プラグインマーケットプレイス定義
├── plugins/
│   ├── with-me/             # ソフトウェア要件抽出プラグイン
│   │   ├── .claude-plugin/  # プラグインメタデータ
│   │   ├── commands/        # スラッシュコマンド定義
│   │   ├── config/          # 設定 (dimensions.json)
│   │   └── with_me/         # Python実装
│   │       ├── cli/         # CLI コマンド
│   │       └── lib/         # コアライブラリ
│   └── lunch-decision/      # ランチ選択プラグイン
│       ├── .claude-plugin/
│       ├── commands/
│       ├── config/          # ランチ用の次元定義
│       └── lunch_decision/  # Python実装
├── tests/                   # プロジェクトレベルテスト
└── mise.toml                # 開発環境定義
```

## Development

### Prerequisites

- Python 3.11+
- [mise](https://mise.run) - Tool version management

### Setup

```bash
# Install mise (if not already installed)
curl https://mise.run | sh

# Install dependencies
mise install
```

### Available Tasks

```bash
mise run lint           # Lint code
mise run format         # Format code
mise run typecheck      # Type check
mise run test           # Run doctests
mise run validate       # Validate plugin configuration
```

### Testing Plugins

```bash
# Initialize with-me session
PYTHONPATH="plugins/with-me" python3 -m with_me.cli.session init

# Initialize lunch-decision session
PYTHONPATH="plugins/lunch-decision" python3 -m lunch_decision.cli.session init

# Verify session structure
mise run test:e2e:verify:session
```

## Creating New Plugins

新しいユースケースに適用する場合：

1. **既存プラグインをコピー**
   ```bash
   cp -r plugins/with-me plugins/your-use-case
   ```

2. **5次元を定義** (`config/dimensions.json`)
   - ユースケースに合わせた次元を設計
   - 各次元の仮説を定義
   - 依存関係 (DAG) を設定

3. **コマンド定義を更新** (`commands/good-question.md`)
   - 説明文をユースケースに合わせて変更
   - CLI コマンドのモジュールパスを更新

4. **Pythonモジュール名を変更**
   ```bash
   mv plugins/your-use-case/with_me plugins/your-use-case/your_module
   ```

5. **marketplace.jsonに追加**

## Configuration

各プラグインの `config/dimensions.json` で調整可能：

- **convergence_threshold** - 収束閾値 (デフォルト: 0.3)
- **max_questions** - 質問数上限
- **min_questions** - 最小質問数
- **importance** - 各次元の重要度

## Documentation

- [Technical Overview](plugins/with-me/docs/technical-overview.md) - アルゴリズムと理論
- [Contributing Guide](CONTRIBUTING.md) - 開発ガイドライン
- [Command Reference](plugins/with-me/commands/good-question.md) - コマンド使用法

## Original Repository

このPoCは以下のリポジトリのwith-meプラグインを参照：
- https://github.com/h315uk3/symbiosis

## License

AGPL-3.0
