# チュートリアル

このページには、Gemini CLI と対話するためのチュートリアルが含まれています。

## モデルコンテキストプロトコル (MCP) サーバーのセットアップ

> [!CAUTION]
> サードパーティの MCP サーバーを使用する前に、そのソースを信頼し、提供されるツールを理解していることを確認してください。サードパーティのサーバーの使用は、ご自身の責任で行ってください。

このチュートリアルでは、[GitHub MCP サーバー](https://github.com/github/github-mcp-server) を例として使用して、MCP サーバーをセットアップする方法を示します。GitHub MCP サーバーは、問題の作成やプルリクエストへのコメントなど、GitHub リポジトリと対話するためのツールを提供します。

### 前提条件

開始する前に、次のものがインストールされ、構成されていることを確認してください。

- **Docker:** [Docker] をインストールして実行します。
- **GitHub 個人用アクセストークン (PAT):** 必要なスコープを持つ新しい [クラシック] または [きめ細かい] PAT を作成します。

[Docker]: https://www.docker.com/
[クラシック]: https://github.com/settings/tokens/new
[きめ細かい]: https://github.com/settings/personal-access-tokens/new

### ガイド

#### `settings.json` で MCP サーバーを構成する

プロジェクトのルートディレクトリで、[`.gemini/settings.json` ファイル](./configuration.md) を作成または開きます。ファイル内に、GitHub MCP サーバーの起動方法を指示する `mcpServers` 構成ブロックを追加します。

```json
{
  "mcpServers": {
    "github": {
      "command": "docker",
      "args": [
        "run",
        "-i",
        "--rm",
        "-e",
        "GITHUB_PERSONAL_ACCESS_TOKEN",
        "ghcr.io/github/github-mcp-server"
      ],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "${GITHUB_PERSONAL_ACCESS_TOKEN}"
      }
    }
  }
}
```

#### GitHub トークンを設定する

> [!CAUTION]
> 個人用およびプライベートリポジトリへのアクセス権を持つ広範囲にスコープが設定された個人用アクセストークンを使用すると、プライベートリポジトリの情報がパブリックリポジトリに漏洩する可能性があります。パブリックリポジトリとプライベートリポジトリの両方へのアクセスを共有しない、きめ細かいアクセストークンを使用することをお勧めします。

環境変数を使用して GitHub PAT を保存します。

```bash
GITHUB_PERSONAL_ACCESS_TOKEN="pat_YourActualGitHubTokenHere"
```

Gemini CLI は、`settings.json` ファイルで定義した `mcpServers` 構成でこの値を使用します。

#### Gemini CLI を起動して接続を確認する

Gemini CLI を起動すると、構成が自動的に読み取られ、バックグラウンドで GitHub MCP サーバーが起動します。その後、自然言語プロンプトを使用して、Gemini CLI に GitHub アクションを実行するように依頼できます。例:

```bash
"「foo/bar」リポジトリで自分に割り当てられているすべてのオープンな問題を取得し、それらを優先順位付けしてください"
```