# AIが読む本フォーマット v0.1

AIが文章の主旨を追跡できるようにするための構造化フォーマット。

テキストを `content_units`・`relations`・`interpretations`・`uncertainties` に分解してYAMLとして記述する。

→ 背景と発見についてはnoteの記事を参照（リンク予定）

---

## ファイル構成

| ファイル | 内容 |
|---|---|
| `AIが読む本フォーマット v0_1.md` | 仕様書・設計思想・実例（小説・エッセイ） |
| `bookSchema.json` | JSON Schema（バリデーション用） |
| `対談構造化例_プロンプト工学.md` | 対話ログへの適用例 |

---

## 基本構造

```yaml
metadata:
  title:
  author:
  genre:
  language:

structure:
  units:
    - id:
      type:      # chapter / section / scene など
      title:

content_units:
  - id:
    type:        # state / event / statement / reflection など
    location:    # structure.units.id を参照
    description: # 記述されていること。解釈を入れない

relations:
  - id:
    source:      # content_units.id
    target:      # content_units.id
    type:        # temporal_sequence / explicit_cause / possible_cause /
                 # retrospective_link / contrast / thematic_echo

interpretations:
  - id:
    agent:       # narrator / reader / critic
    target:
    claim:
    confidence:  # low / medium / high

uncertainties:
  - id:
    target:
    type:        # causal_unknown / mechanism_unknown / evidence_missing /
                 # witness_unavailable / scope_unknown / interpretation_conflict
    reason:
```

---

## 設計原則

- `content_units` には記述されていることだけを入れる。解釈は `interpretations` へ
- 不確定な領域は削除せず `uncertainties` として保存する
- 解釈には必ず主体（`agent`）を付ける
- 因果は確定のものだけでなく候補関係も `possible_cause` として記録する

---

## バリデーション

```bash
npm install -g ajv-cli
ajv validate -s bookSchema.json -d your_file.yaml
```

---

## 拡張

`format_rules` フィールドで relation type や agent の語彙を追加定義できる。対話ログへの適用例（`ironic_echo` など）は `対談構造化例_プロンプト工学.md` を参照。

---

## ライセンス

MIT
