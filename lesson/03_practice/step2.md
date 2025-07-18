# Roleを使って実用的なPlaybookを実装する

まずは以下のコマンドを実行してください。

```bash
ansible-playbook -i inventory playbook_short_sample.yaml
```

正常に実行完了したら、`~/ansible-training/exercise/03_practice`ディレクトリ直下にある`playbook_short_sample.yaml`ファイルを開いてください。  
中身を見ると、1つのPlaybookファイルにTaskが直接記載されており、このファイルのみで実行内容が完結していることがわかります。  
Playbookは実はこのようにとてもシンプルな構成で実装することが可能です。  
簡易的な自動化であればこれでも特に問題はありません。  

しかし、実用的なPlaybookでは複数のTaskを組み合わせて多くの設定の構成管理や複雑な自動化を行うため、
この構成ですべてのTaskを1つのPlaybookに実装してしまうとファイルが徐々に肥大化していきます。  
肥大化したPlaybookはいわゆるスパゲティコードと呼ばれる解読困難なPlaybookになりがちで、バグが埋め込まれていても気付きにくく、
再利用したくても実行したら何が起こるのか怖くて安易に再利用できないものとなってしまいます。  
Ansibleではこれを解消する仕組みの1つとして、Roleと呼ばれる概念が存在しています。

## Roleの考え方について

Roleとは、一般的なオブジェクト指向プログラミングでいうところの「カプセル化」に近い考え方です。  
カプセル化をすることでそのオブジェクトの「目的と範囲」、実装すべき「処理」、必要な「入力値」が明確になり、保守管理しやすく再利用しやすいコードを実装することができます。  
Ansibleに言い換えると、例えば簡易的には以下のようになります。

* 目的：PostgreSQLを稼働した状態にする
* 処理：PostgreSQLのインストール、設定変更、サービス起動
* 入力値：PostgreSQLの各種パラメータ

このRoleは明らかにPostgreSQLの構成管理を行うことを目的としたRoleであるとわかり、可読性が高くて使い方のわかりやすい（＝再利用しやすい）コードとなります。  
実用的なPlaybookには、このような保守管理しやすくて再利用性の高い設計と実装が求められます。

## クイズ

若干難易度の高いクイズになっています。正解は次のページにあります。

1. 以下の選択肢のうち、Roleについて「間違っている」記述はどれ？

- [ ] サーバごとに異なるパラメータで処理を実行できる
- [ ] 複数のTaskを定義できる
- [ ] 実行対象のサーバを定義できる
- [ ] 1つのRoleを複数のPlaybookで利用できる

2. 以下の選択肢のうち、Roleを利用する「メリットでない」ものはどれ？

- [ ] 処理内容がわかりやすくなる
- [ ] 実行時に指定の必要なパラメータがわかりやすくなる
- [ ] コードを再利用しやすくなる
- [ ] 多くの機能を1つのRoleに一元化できて管理しやすくなる
- [ ] 機能の拡張がしやすくなる

3. 以下の選択肢のうち、Role実装時に注意することはどれ？

- [ ] なるべく目的の粒度は大きくする
- [ ] なるべく処理（Task）の個数は少なくする
- [ ] なるべく変数は使わずに固定値を埋め込む
- [ ] なるべくディレクトリ構成はテンプレート通りにする

---

- [前のページに戻る](step1.md)
- [目次](README.md)
- [解説に進む](step2a.md)
