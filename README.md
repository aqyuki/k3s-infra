# README

## Summary

このリポジトリでは、自宅サーバで運用している[k3s](https://k3s.io/)のマニフェストや設定などを管理しています。

## 🔐 Secret

### Secretの定義方法

KubernetesのSecretは、対象の値を**Base64エンコード**して定義します。
エンコードを行う際は、以下のコマンドを利用してください。

```bash
echo -n "target value" | openssl enc -e -base64
```

### Secretの暗号化

Secretに当たる情報は[sealed-secrets](https://github.com/bitnami-labs/sealed-secrets)を利用して暗号化してGitHubにアップロードしてください。

原則、暗号化後のファイル名は`sealed-secret.yaml`とし、暗号化前のファイル名は`secret.yaml`としてください。
ただし、暗号化するファイルが複数に渡る際などは適切に分割してください。その際には、`.gitignore`に追加することを忘れないでください。

```bash
# encrypt
kubeseal --format=yaml --cert=cert.pem < secret.yaml > sealed-secret.yaml
```

### Applicationの管理

k3sにデプロイされるアプリケーションはArgoCDによってデプロイされます。デプロイする際には、app以下に適当なアプリケーションマニフェストを作成してください。
GitHubにpushするとArgo CDが自動で検出してデプロイします。
