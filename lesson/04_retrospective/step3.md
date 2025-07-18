Start - [1](step1.md) - [2](step2.md) - [**3**](step3.md) - [4](step4.md) - [5](step5.md) - [6](step6.md) - [7](step7.md) - [8](step8.md) - End


# 課題2: 基本的なPlaybookの作成

## 以降の課題の進め方について

`exercise/04_retrospective`に最低限のファイルを配置してあるため、基本的にはこのディレクトリの各ファイルを編集して順番通りに課題を進めていくことを想定しています。  
ただし、自分がやりたいところだけをやったり、課題ごとにPlaybookやRoleのファイルを作成していくなどの進め方でも問題ありません。

## 課題2-1: ユーザを作成する

`user`モジュールを使って各サーバに`nginx`という名前のユーザを作成してください。  
名前以外のオプションは任意でよいです。  
適当に変更してみてどこが変わるのかを確認してみてください。

※補足  
今回の処理は以下のように`ansible-playbook`コマンド実行時に`-b`オプションを付与しないと権限不足でエラーになります。  
`<Playbookファイル>`の部分は各自作成したファイル名に合わせてください。  
以降の課題でもユーザ作成を行いますが、いずれも`-b`オプションが必要です。

```bash
ansible-playbook -i inventory <Playbookファイル> -b
```

## 課題2-2: 作成したユーザの確認

アドホックコマンドを使って、各サーバに`nginx`ユーザが作成されたことを確認してください。  
ユーザの存在確認方法はいくつかありますが、どの方法でもよいです。

## 発展課題: becomeについて

`-b`オプションは`become`と呼ばれるオプションです。  
この`become`の意味について[公式ドキュメント](https://docs.ansible.com/ansible-core/2.15_ja/playbook_guide/playbooks_privilege_escalation.html#playbooks-privilege-escalation)などを参考にして調べ、なぜ`become`を有効にしないと実行できないのかを考えてみてください。  
なお、`-b`オプションを付与する以外にも、Playbook等で`become: yes`と記載しても同様の効果があります。

---

- [前のページに戻る](step2a.md)
- [目次](README.md)
- [解説に進む](step3a.md)
