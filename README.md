# action-push-ghpages

（日本語が後に続きます）

Push specified static assets to the gh-pages branch

このGitHub Actionは、指定した静的ファイル群を含んだコミットを作り、`gh-pages` ブランチに push します。  
sourceを `gh-pages` ブランチに設定することで、GitHub Pagesとして公開できます。

## Inputs

### `build_dir`

**必須** 静的ファイル群が置かれているディレクトリへのパスです。  
リポジトリのルートからの相対パスで指定してください。

### `github_token`

**必須** `secrets.GITHUB_TOKEN` を指定してください。  
リポジトリにpushする際に使います。

## Example Usage

```yaml
steps:
  - name: Checkout code
    uses: actions/checkout@v2
  - name: Set up Python 3.10
    uses: actions/setup-python@v2
    with:
      python-version: "3.10"
  - name: Install dependencies
    run: |
      python -m pip install -U pip
      python -m pip install -r requirements.txt
  - name: Build html
    run: |
      make html
      rm -r build/html/_sources
  - name: Publish on GitHub Pages
    uses: ftnext/action-push-ghpages@v1.0.0
    with:
      build_dir: build/html
      github_token: ${{ secrets.GITHUB_TOKEN }}
```

ref: https://github.com/ftnext/awesome-sing-a-bit-of-harmony/blob/49e9f0c6fa4968345b4ff31057b01e53a0bea471/.github/workflows/publish-pages.yml#L10-L29
