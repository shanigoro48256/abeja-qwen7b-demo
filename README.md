## VS Code からリモート GPU インスタンスへ接続する場合

`.ssh/config` に次のブロックを追加しておくと、  
VS Code の **Remote-SSH** 拡張機能からワンクリックで  
ポートフォワードができます。

```sshconfig
Host sample                 # 任意のホスト名
    HostName <インスタンスのIP>      # 例: 203.0.113.10
    Port 10022                   # インスタンス側 SSH ポート
    User buser                   # リモートのユーザー名
    IdentityFile ~/.ssh/ackey.txt    # 秘密鍵 (ローカルパス)
    ProxyCommand C:/Windows/System32/OpenSSH/ssh.exe ^
        -W %h:%p -i ~/.ssh/ackey.txt -p 30022 user@as-highreso.com
    LocalForward 8888 localhost:8888   # Jupyter Lab をローカル 8888 に転送
````
---

## セットアップ

```bash
# 1) リポジトリを取得
git clone https://github.com/shanigoro48256/abeja-qwen7b-demo.git
cd abeja-qwen7b-demo

# 2) コンテナをビルドして起動 (初回はビルドに数分かかります)
docker compose up           # -d を付けるとバックグラウンド起動
```

---

## Jupyter Lab の利用

1. `.ssh/config` で転送設定済みなら VS Code Remote-SSH で接続、
   ローカル実行ならそのままブラウザを開きます。
2. アドレスバーに **[http://localhost:8888/](http://localhost:8888/)** と入力。
3. `demo.ipynb` を開き、セルを上から順に実行して
  ABEJA-Qwen2.5-7b-Japanese-v0.1 の推論を行います。

## ファイル構成

```text
.
├─ Dockerfile            # 実行環境定義
├─ docker-compose.yml    # サービス定義
├─ demo.ipynb            # サンプル Notebook
├─ .gitignore            # キャッシュ等を除外
└─ .dockerignore         # イメージに含めないファイル
```

## ライセンス

| 対象 | ライセンス | 備考 |
|------|-----------|------|
| ABEJA-Qwen2.5-7b-Japanese-v0.1 モデル | Apache License 2.0 | 詳細は <https://huggingface.co/abeja/ABEJA-Qwen2.5-7b-Japanese-v0.1/blob/main/LICENSE> を参照 |
| Qwen/Qwen2.5 ベースモデル | Apache License 2.0 | Alibaba Cloud が公開する Qwen 系列モデルのライセンス |

> **注意**  
> - モデルを商用利用する場合は **Apache-2.0** の条項に従ってください。  


