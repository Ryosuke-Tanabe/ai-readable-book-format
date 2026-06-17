AIが読む本フォーマット v0.1
1. 概要

AIが本の内容を構造的に扱えるようにするためのフォーマット。

目的は意味を一つに固定することではなく、以下を分離して保存することにある。

本文で記述された内容

それに対する解釈

未確定の領域

対象ジャンル：

小説

エッセイ

論文

思想書

回想録

2. 設計思想

このフォーマットの基本原則：

fact と interpretation を分離する

uncertainty を内容として保存する

解釈には主体を付ける

因果は断定せず候補関係も保存する

構造は意味を固定するためではなく、意味の可能性と限界を保存するために使う

3. コア構造

v0.1では以下の6要素をコアとする。

metadata
structure
content_units
interpretations
uncertainties
relations
4. 各要素仕様
metadata

書誌情報。

metadata:
  title:
  author:
  genre:
  language:
structure

本文の配置構造。
意味構造ではなく章や節などの区切りを示す。

structure:
  units:
    - id:
      type:
      title:

例：

chapter

section

part

scene

content_units

本文に記述されている内容の最小単位。

重要ルール：

description must describe what is stated, observed, or explicitly reported, not inferred meaning

つまり以下のみを記録する。

出来事

観察

発言

状態

解釈はここに入れない。

content_units:
  - id:
    type:
    location:
    description:
interpretations

主体付きの解釈レコード。

interpretations:
  - id:
    agent:
    target:
    claim:
    confidence:
agent（v0.1）
narrator
reader
critic
confidence
low
medium
high
uncertainties

不確定性を保存する層。

uncertainties:
  - id:
    target:
    type:
    reason:

推奨タイプ：

causal_unknown
mechanism_unknown
evidence_missing
witness_unavailable
scope_unknown
interpretation_conflict
relations

content_units間の関係。

relations:
  - id:
    source:
    target:
    type:

v0.1 relation type：

temporal_sequence
explicit_cause
possible_cause
retrospective_link
contrast
thematic_echo
5. 推奨語彙

content_units.type の推奨セット：

state
event
observation
statement
outcome
condition
trigger
reflection

これは必須語彙ではなく recommended vocabulary。

6. 設計原則

fact と interpretation を分離する

uncertainty を内容として保存する

解釈主体を記録する

relations は確定因果だけでなく候補関係も扱う

構造は意味を固定するためではなく 意味の可能性と限界を保持するために使う

7. v0.2検討事項

将来の拡張候補。

content_units.type語彙体系

agent粒度の細分化

relations.type拡張

confidence数値化

Appendix

実例は [`お不動さん.md`](お不動さん.md) を参照。

