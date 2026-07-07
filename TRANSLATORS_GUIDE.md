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

### 6. Inline HTML in Markdown

Please do not add or modify inline HTML tags in markdown translation strings.

If a string already contains HTML, keep tags exactly as they are and only translate human-readable text.

## What SHOULD Be Translated

Translate:
- ✅ Regular text and paragraphs
- ✅ Headings and titles
- ✅ Button text (the `text` parameter value)
- ✅ Alt text for images
- ✅ Link text that appears to users
- ✅ Descriptions and instructions

Do NOT translate/modify:
- ❌ Shortcode names and shortcode syntax (`{{< ... >}}`)
- ❌ Pipe variables (`|version|`, `|ltrversion|`, etc.)
- ❌ URLs and file paths used for linking
- ❌ Inline HTML tags (`<span>`, `<br/>`, `<div>`, etc.)

## Examples

### Example 1: User Groups Link

**English Source:**
```markdown
See [User Groups]({{< ref "community/groups.md" >}}) to read more.
```

**✅ Correct Bulgarian Translation:**
```markdown
Вижте [Потребителски групи]({{< ref "community/groups.md" >}}) за да прочетете повече.
```

Note: Only "User Groups" and "to read more" are translated. The file path stays in English.

### Example 2: Button with Link

**English Source:**
```markdown
{{< button class="is-primary1" link="community/groups" text="User groups 🇩🇪 🇫🇷 🇪🇸" >}}
```

**✅ Correct Bulgarian Translation:**
```markdown
{{< button class="is-primary1" link="community/groups" text="Потребителски групи 🇩🇪 🇫🇷 🇪🇸" >}}
```

Note: Only the `text` value is translated. Everything else (shortcode name, class, link path) remains in English.

### Example 3: Image Gallery

**English Source:**
```markdown
{{< hub-images showcase="map" quantity="4" columns="gallery" >}}
```

**✅ Correct Translation (ANY language):**
```markdown
{{< hub-images showcase="map" quantity="4" columns="gallery" >}}
```

Note: This entire shortcode stays the same in ALL languages - nothing should be translated!

### Example 4: Tab Labels with Hugo Variables

**English Source:**
```markdown
{{<tabs tab1="QGIS |ltrversion|" tab2="QGIS testing (>|version|)" tab3="Archived releases" >}}
```

**✅ Correct Bulgarian Translation:**
```markdown
{{<tabs tab1="QGIS |ltrversion|" tab2="QGIS тестване (>|version|)" tab3="Архивирани издания" >}}
```

**❌ WRONG Bulgarian Translation:**
```markdown
{{<tabs tab1="QGIS |алтернативна версия|" tab2="QGIS тестване (>|версия|)" tab3="Архивирани издания" >}}
```

Note: You can translate "QGIS testing" → "QGIS тестване" and "Archived releases" → "Архивирани издания", but the pipe-delimited variables (`|ltrversion|`, `|version|`) must stay exactly as they are!

## Why This Matters

When technical content gets translated:
- 🚫 The website build fails
- 🚫 Links stop working
- 🚫 Images don't display
- 🚫 Layout breaks

Our automated system will fix some of these issues, but it's better to avoid them in the first place!

## Questions?

If you're unsure whether something should be translated:
- **If it looks like code or a file path** → Don't translate it
- **If it's inside `{{< >}}` brackets** → Usually don't translate it (except `text` and similar display values)
- **If users will see it on the website** → Translate it

When in doubt, ask the translation coordinators or check the English source to see what's meant for display vs. technical markup.

Thank you for helping make QGIS accessible to speakers of your language! 🌍
