# QGIS ウェッブサイト翻訳者用ガイド

## ⚠️ 重要: 技術コンテンツは翻訳しないで下さい

QGISウェブサイトのコンテンツを翻訳する際は、以下の技術的な要素を翻訳 **しないで** ください。:

### 1. Hugo ショートコード (Tags)

ショートコードは、Hugoがウェブサイトの機能を生成するために使用する特別なマークアップです。これらは `{{< >}}` または `{{% %}}` で囲まれます。

**❌ 間違い:**
```markdown
{{< край на колоната >}}  <!-- Bulgarian translation of "column-end" -->
{{< fin de colonne >}}     <!-- French translation of "column-end" -->
```

**✅ 正解:**
```markdown
{{< column-end >}}        <!-- Always keep in English -->
```

### 2.リンク内のファイルパス

`ref` ショートコード内のファイルパスは、英語のままにする必要があります。:

**❌ 間違い:**
```markdown
{{< ref "общност/групи.md" >}}        <!-- Translated path -->
{{< ref "communauté/groupes.md" >}}   <!-- Translated path -->
```

**✅ 正解:**
```markdown
{{< ref "community/groups.md" >}}     <!-- Always keep in English -->
```

### 3. ショートコードのパラメータ値

技術パラメータの値は英語のままにする必要があります。:

**❌ 間違い:**
```markdown
{{< hub-images showcase="карта" columns="галерия" >}}
{{< column-start class="заоблена" >}}
```

**✅ 正解:**
```markdown
{{< hub-images showcase="map" columns="gallery" >}}
{{< column-start class="rounded" >}}
```

### 4. URLセグメントとリンク

URLパスや技術的な識別子を見つけた場合は、英語のままにしてください。:

**❌ 間違い:**
```markdown
{{< button link="общност/групи" text="Потребителски групи" >}}
```

**✅ 正解:**
```markdown
{{< button link="community/groups" text="Потребителски групи" >}}
```

`text` パラメータのみを翻訳してください！

### 5. Hugoのテンプレート変数

Hugoでは、バージョン番号などの動的なコンテンツに `|variable|` というパイプ記法が使用されます。これらの変数名は、 **決して** 翻訳してはなりません。

**❌ 間違い:**
```markdown
QGIS |алтернативна версія|      <!-- Ukrainian: "alternative version" -->
QGIS |versión ltr|              <!-- Spanish variation -->
```

**✅ 正解:**
```markdown
QGIS |ltrversion|               <!-- Variable name stays in English -->
```

よく目にするHugoの変数：
- `|version|` - 現在のQGISバージョン
- `|ltrversion|` - 長期リリース版
- `|nextversion|` - 次期バージョン

**✅ これらの変数の「周囲」にあるテキストは翻訳可能です:**
```markdown
English:    QGIS |ltrversion|
Bulgarian:  QGIS |ltrversion|         (keep "QGIS" or translate if needed)
Spanish:    QGIS |ltrversion|         (keep "QGIS" or translate if needed)
```

重要なルール: **パイプ（|...|）で囲まれたテキストは変数名です。絶対に翻訳しないでください！**

### 6. Markdown内のインラインHTML

Markdownの翻訳文字列において、インラインHTMLタグを追加または変更しないでください。

文字列にすでにHTMLが含まれている場合は、タグはそのまま維持し、人間が読むテキストのみを翻訳してください。

## 翻訳すべきもの

翻訳する:
- ✅ 通常のテキストと段落
- ✅ 見出しとタイトル
- ✅ ボタンのテキスト（`text` パラメーターの値）
- ✅ 画像の代替テキスト
- ✅ ユーザーに表示されるリンクテキスト
- ✅ 説明と手順

翻訳/変更してはいけない:
- ❌ ショートコード名とショートコードの構文 (`{{< ... >}}`)
- ❌ パイプ変数（`|version|`、`|ltrversion|` など）
- ❌ リンクに使用されるURLおよびファイルパス
- ❌ インラインHTMLタグ（`<span>`、`<br/>`、`<div>`など）

## 例

### 例 1: User Groups Link

**英語ソース:**
```markdown
See [User Groups]({{< ref "community/groups.md" >}}) to read more.
```

**✅ 正しい Bulgarian 翻訳:**
```markdown
Вижте [Потребителски групи]({{< ref "community/groups.md" >}}) за да прочетете повече.
```

注："User Groups" と "to read more" のみ翻訳されています。ファイルパスは英語のままです。

### 例 2: Button with Link

**英語ソース:**
```markdown
{{< button class="is-primary1" link="community/groups" text="User groups 🇩🇪 🇫🇷 🇪🇸" >}}
```

**✅ 正しい Bulgarian 翻訳:**
```markdown
{{< button class="is-primary1" link="community/groups" text="Потребителски групи 🇩🇪 🇫🇷 🇪🇸" >}}
```

注: `text` の値のみが翻訳されます。それ以外（ショートコード名、クラス、リンクパス）は英語のままとなります。

### 例 3: Image Gallery

**英語ソース:**
```markdown
{{< hub-images showcase="map" quantity="4" columns="gallery" >}}
```

**✅ 正しい翻訳 (任意の言語):**
```markdown
{{< hub-images showcase="map" quantity="4" columns="gallery" >}}
```

注：このショートコード全体は、すべての言語において変更されません。翻訳しないでください。

### 例 4: Tab Labels with Hugo Variables

**英語ソース:**
```markdown
{{<tabs tab1="QGIS |ltrversion|" tab2="QGIS testing (>|version|)" tab3="Archived releases" >}}
```

**✅ 正しい Bulgarian 翻訳:**
```markdown
{{<tabs tab1="QGIS |ltrversion|" tab2="QGIS тестване (>|version|)" tab3="Архивирани издания" >}}
```

**❌ 間違った Bulgarian 翻訳:**
```markdown
{{<tabs tab1="QGIS |алтернативна версия|" tab2="QGIS тестване (>|версия|)" tab3="Архивирани издания" >}}
```

注："QGIS testing" を "QGIS тестване"、"Archived releases" を "Архивирани издания" と翻訳することは可能ですが、パイプで区切られた変数（`|ltrversion|`、`|version|`）は、そのまま変更せずに残す必要があります。

## これが重要な理由

技術的なコンテンツが翻訳されると:
- 🚫 ウェブサイトのビルドが失敗します
- 🚫 リンクが機能しなくなる
- 🚫 画像が表示されません
- 🚫 レイアウト崩れ

我々の自動システムがこうした問題の一部を修正しますが、そもそも発生させないようにするのが最善です。

## 質問?

何かを翻訳すべきかどうか迷っている場合:
- **コードやファイルパスのように見える場合** → 翻訳しないでください
- **`{{< >}}` 括弧内にある場合** → 通常は翻訳しません（`text` やそれに類する表示用値は除く）。
- **ユーザーがウェブサイト上で目にする場合** → 翻訳してください

判断に迷う場合は、翻訳コーディネーターに尋ねるか、英語の原文を確認して、何が表示用で何が技術的なマークアップなのかを確かめてください。

QGISをあなたの言語の話し手にとって利用しやすいものにするためのご協力、ありがとうございます！ 🌍
