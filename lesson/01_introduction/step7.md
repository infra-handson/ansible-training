Start - [1](step1.md) - [2](step2.md) - [3](step3.md) - [4](step4.md) - [5](step5.md) - [6](step6.md) - [**7**](step7.md) - End

# インベントリにターゲットを追加する

インベントリファイルに3号機の情報を追加してWebサーバ構築のPlaybookを再実行します。

## 1. インベントリへの追加

インベントリファイル（`01_introduction/inventory`）をエディタで開き、`target01`, `target02`を参考にして`target03`を追加してください。  
`target03`として記載する内容は以下になります。<kbd>Ctrl</kbd>+<kbd>S</kbd>でファイル保存するのを忘れないようにご注意ください。

```yaml
    target03:
      ansible_port: 2224
      ansible_user: john
```

ファイルを保存したら以下のコマンドでインベントリファイルを確認します。

```bash
ansible-inventory -i inventory --list -y
```

以下の出力がされたらインベントリファイルへの追加は完了です。  
インデント（スペースの個数）が大事になるため、以下と同じ出力にならない場合は同じになるように編集し直してください。

```yaml
all:
  children:
    ungrouped:
      hosts:
        target01:
          ansible_port: 2222
          ansible_ssh_private_key_file: ~/.ssh/test_key
          ansible_user: hoge
        target02:
          ansible_port: 2223
          ansible_ssh_private_key_file: ~/.ssh/test_key
          ansible_user: foo
        target03:
          ansible_port: 2224
          ansible_ssh_private_key_file: ~/.ssh/test_key
          ansible_user: john
```

## 2. Playbookの再実行

以下のコマンドを実行してください。

```bash
ansible-playbook -i inventory playbook_nginx.yaml
```

実行が完了したら、先程と同様に3号機のページ（`演習環境のURL:8084`）へアクセスしてページが表示されることを確認します。  
なお、Playbookの再実行で1号機と2号機はすべて`ok`または`skipping`となっており、`changed`が1つも発生していないことが確認できるかと思います。  
これがAnsibleの特徴である「**冪等性**（べきとうせい）」と呼ばれる性質であり、「すでに定義通りの状態になっていたら何もしない」ことを表しています。

## 3. クイズ

テキストでは特に触れていませんが、上記のインベントリファイルからどんなことが読み取れるでしょうか？  
逆に言えば、インベントリファイルにはどんな情報が必要だと考えられるでしょうか？  
以下から正しいと思われる選択肢を選んでください。

1. **上記のインベントリファイルから読み取れる、正しい説明を選択してください**
    - [ ] このインベントリには5台まで定義することができる
    - [ ] このインベントリはYaml形式で書かれている
    - [ ] このインベントリはWebサーバ構築用のPlaybookでしか使われない
2. **上記のインベントリファイルから読み取れる、『接続情報』を選択してください**
    - [ ] ターゲットへ接続する際のIP
    - [ ] ターゲットへ接続する際のパスワード
    - [ ] ターゲットへ接続する際のユーザ名
3. **上記のインベントリファイルから読み取れる、『認証方式』を選択してください**
    - [ ] 公開鍵認証方式
    - [ ] パスワード認証方式
    - [ ] Ansible独自の認証方式

---

- [前のページに戻る](step6.md)
- [目次](README.md)
- [クイズ解説に進む](step7a.md)
