# Web フェッチツール (`web_fetch`)

このドキュメントでは、Gemini CLI の `web_fetch` ツールについて説明します。

## 説明

`web_fetch` を使用して、Web ページから情報を要約、比較、または抽出します。`web_fetch` ツールは、プロンプトに埋め込まれた 1 つ以上の URL (最大 20) からコンテンツを処理します。`web_fetch` は自然言語のプロンプトを受け取り、生成された応答を返します。

### 引数

`web_fetch` は 1 つの引数を取ります。

- `prompt` (文字列、必須): フェッチする URL (最大 20) とそのコンテンツの処理方法に関する具体的な指示を含む包括的なプロンプト。例: `"https://example.com/article を要約し、https://another.com/data からキーポイントを抽出してください"`。プロンプトには、`http://` または `https://` で始まる URL が少なくとも 1 つ含まれている必要があります。

## Gemini CLI で `web_fetch` を使用する方法

Gemini CLI で `web_fetch` を使用するには、URL を含む自然言語のプロンプトを指定します。ツールは、URL をフェッチする前に確認を求めます。確認されると、ツールは Gemini API の `urlContext` を介して URL を処理します。

Gemini API が URL にアクセスできない場合、ツールはローカルマシンから直接コンテンツをフェッチするようにフォールバックします。ツールは、可能な場合はソースの帰属と引用を含め、応答をフォーマットします。その後、ツールはユーザーに応答を提供します。

使用法:

```
web_fetch(prompt="https://google.com などの URL を含むプロンプト")
```

## `web_fetch` の例

単一の記事を要約します。

```
web_fetch(prompt="https://example.com/news/latest の要点を要約できますか")
```

2 つの記事を比較します。

```
web_fetch(prompt="これら 2 つの論文の結論の違いは何ですか: https://arxiv.org/abs/2401.0001 と https://arxiv.org/abs/2401.0002?")
```

## 重要な注意事項

- **URL 処理:** `web_fetch` は、指定された URL にアクセスして処理する Gemini API の機能に依存します。
- **出力品質:** 出力の品質は、プロンプト内の指示の明確さに依存します。