# 課題2: 基本的なPlaybookの作成

## 課題2-1: ユーザを作成する

taskのみ記載します。

```yaml
- name: ユーザ作成
  user:
    name: "nginx"
    state: present
```

## 課題2-2: 作成したユーザの確認

コマンド例として、以下のような確認方法があります。

```bash
ansible -m shell -a "id nginx" -i inventory all
```

```bash
ansible -m shell -a "tail /etc/passwd" -i inventory all
# catでもよいが、出力行が多いのでtailの方が無難
```

```bash
ansible -m shell -a "grep nginx /etc/passwd" -i inventory all
```

## 補足課題: becomeについて

`become`を有効化すると、リモート先でのタスク実行が`root`ユーザ権限で行われるようになります。  
今回Ansible接続に使用しているユーザは権限が低く、OSにユーザ作成を行う権限がありませんが、`become`を有効化することでユーザ作成の実行が可能になります。  
なお、`become`は`sudo`権限が与えられているユーザでないと実行できません。  
ユーザ権限やユーザの使い分け方等の話はAnsibleではなくLinuxについての理解を深める必要があり、今回の学習の範囲を超えるため、ここでは記載しません。

---

- [前のページに戻る](step3.md)
- [目次](README.md)
- [次のページに進む](step4.md)
