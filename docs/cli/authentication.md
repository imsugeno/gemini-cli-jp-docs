## 認証設定

Gemini CLI では、Google の AI サービスで認証する必要があります。初回起動時に、次のいずれかの認証方法を構成する必要があります。

1.  **Google でログイン (Gemini Code Assist):**

    - このオプションを使用して、Gmail、Google フォト、Google ドライブなどのサービスで個人使用のために使用する標準の個人アカウント (例: your-name@gmail.com) でログインします。
    - 初回起動時に、Gemini CLI は認証のために Web ページにリダイレクトします。認証されると、資格情報がローカルにキャッシュされるため、後続の実行では Web ログインをスキップできます。
    - Web ログインは、Gemini CLI が実行されているマシンと通信できるブラウザで行う必要があることに注意してください。(具体的には、ブラウザは Gemini CLI がリッスンしている localhost URL にリダイレクトされます)。

2.  **Gemini API キー:**

    - Google AI Studio から API キーを取得します: [https://aistudio.google.com/app/apikey](https://aistudio.google.com/app/apikey)
    - `GEMINI_API_KEY` 環境変数を設定します。次の方法では、`YOUR_GEMINI_API_KEY` を Google AI Studio から取得した API キーに置き換えます。
      - 次のコマンドを使用して、現在のシェルセッションで環境変数を一時的に設定できます。
        ```bash
        export GEMINI_API_KEY="YOUR_GEMINI_API_KEY"
        ```
      - 繰り返し使用する場合は、環境変数を `.env` ファイル (プロジェクトディレクトリまたはユーザーホームディレクトリにある) またはシェルの構成ファイル (`~/.bashrc`、`~/.zshrc`、`~/.profile` など) に追加できます。たとえば、次のコマンドは環境変数を `~/.bashrc` ファイルに追加します。
        ```bash
        echo 'export GEMINI_API_KEY="YOUR_GEMINI_API_KEY"' >> ~/.bashrc
        source ~/.bashrc
        ```

3.  **Google Workspace でログイン**

    - このオプションを使用して、**Google Workspace アカウント**でログインします。これは、カスタムメールドメイン (例: your-name@your-company.com)、強化されたセキュリティ機能、管理コントロールなど、一連の生産性向上ツールを提供する企業および組織向けの有料サービスです。これらのアカウントは、多くの場合、雇用主または学校によって管理されています。
      - Google Workspace アカウントは、まず使用する Google Cloud プロジェクト ID を構成し、[Gemini for Cloud API を有効にし](https://cloud.google.com/gemini/docs/discover/set-up-gemini#enable-api)、[アクセス許可を構成する](https://cloud.google.com/gemini/docs/discover/set-up-gemini#grant-iam) 必要があります。次のコマンドを使用して、現在のシェルセッションで環境変数を一時的に設定できます。
      ```bash
      export GOOGLE_CLOUD_PROJECT_ID="YOUR_PROJECT_ID"
      ```
      - 繰り返し使用する場合は、環境変数を `.env` ファイル (プロジェクトディレクトリまたはユーザーホームディレクトリにある) またはシェルの構成ファイル (`~/.bashrc`、`~/.zshrc`、`~/.profile` など) に追加できます。たとえば、次のコマンドは環境変数を `~/.bashrc` ファイルに追加します。
      ```bash
      echo 'export GOOGLE_CLOUD_PROJECT_ID="YOUR_PROJECT_ID"' >> ~/.bashrc
      source ~/.bashrc
      ```
    - 起動時に、Gemini CLI は認証のために Web ページにリダイレクトします。認証されると、資格情報がローカルにキャッシュされるため、後続の実行では Web ログインをスキップできます。
    - Web ログインは、Gemini CLI が実行されているマシンと通信できるブラウザで行う必要があることに注意してください。(具体的には、ブラウザは Gemini CLI がリッスンしている localhost URL にリダイレクトされます)。

4.  **Vertex AI:**
    - エクスプレスモードを使用しない場合:
      - Google Cloud プロジェクトがあり、Vertex AI API を有効にしていることを確認します。
      - 次のコマンドを使用して、アプリケーションのデフォルト資格情報 (ADC) を設定します。
        ```bash
        gcloud auth application-default login
        ```
        詳細については、[Google Cloud のアプリケーションのデフォルト資格情報を設定する](https://cloud.google.com/docs/authentication/provide-credentials-adc) を参照してください。
      - `GOOGLE_CLOUD_PROJECT`、`GOOGLE_CLOUD_LOCATION`、および `GOOGLE_GENAI_USE_VERTEXAI` 環境変数を設定します。次の方法では、`YOUR_PROJECT_ID` と `YOUR_PROJECT_LOCATION` をプロジェクトの関連する値に置き換えます。
        - 次のコマンドを使用して、現在のシェルセッションでこれらの環境変数を一時的に設定できます。
          ```bash
          export GOOGLE_CLOUD_PROJECT="YOUR_PROJECT_ID"
          export GOOGLE_CLOUD_LOCATION="YOUR_PROJECT_LOCATION" # 例: us-central1
          export GOOGLE_GENAI_USE_VERTEXAI=true
          ```
        - 繰り返し使用する場合は、環境変数を `.env` ファイル (プロジェクトディレクトリまたはユーザーホームディレクトリにある) またはシェルの構成ファイル (`~/.bashrc`、`~/.zshrc`、`~/.profile` など) に追加できます。たとえば、次のコマンドは環境変数を `~/.bashrc` ファイルに追加します。
          ```bash
          echo 'export GOOGLE_CLOUD_PROJECT="YOUR_PROJECT_ID"' >> ~/.bashrc
          echo 'export GOOGLE_CLOUD_LOCATION="YOUR_PROJECT_LOCATION"' >> ~/.bashrc
          echo 'export GOOGLE_GENAI_USE_VERTEXAI=true' >> ~/.bashrc
          source ~/.bashrc
          ```
    - エクスプレスモードを使用する場合:
      - `GOOGLE_API_KEY` 環境変数を設定します。次の方法では、`YOUR_GOOGLE_API_KEY` をエクスプレスモードで提供される Vertex AI API キーに置き換えます。
        - 次のコマンドを使用して、現在のシェルセッションでこれらの環境変数を一時的に設定できます。
          ```bash
          export GOOGLE_API_KEY="YOUR_GOOGLE_API_KEY"
          export GOOGLE_GENAI_USE_VERTEXAI=true
          ```
        - 繰り返し使用する場合は、環境変数を `.env` ファイル (プロジェクトディレクトリまたはユーザーホームディレクトリにある) またはシェルの構成ファイル (`~/.bashrc`、`~/.zshrc`、`~/.profile` など) に追加できます。たとえば、次のコマンドは環境変数を `~/.bashrc` ファイルに追加します。
          ```bash
          echo 'export GOOGLE_API_KEY="YOUR_GOOGLE_API_KEY"' >> ~/.bashrc
          echo 'export GOOGLE_GENAI_USE_VERTEXAI=true' >> ~/.bashrc
          source ~/.bashrc
          ```