# README

## Summary

このリポジトリでは、自宅サーバで運用している[k3s](https://k3s.io/)のマニフェストや設定などを管理しています。

## 🔐 Secret

Secretに当たる情報は[sealed-secrets](https://github.com/bitnami-labs/sealed-secrets)を利用して暗号化してGitHubにアップロードしてください。

原則、暗号化後のファイル名は`sealed-secret.yaml`とし、暗号化前のファイル名は`secret.yaml`としてください。
ただし、暗号化するファイルが複数に渡る際などは適切に分割してください。その際には、`.gitignore`に追加することを忘れないでください。

```bash
# encrypt
kubeseal --format=yaml --cert=cert.pem < secret.yaml > sealed-secret.yaml
```
