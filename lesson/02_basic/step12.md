Start - [1](step01.md) - [2](step02.md) - [3](step03.md) - [4](step04.md) - [5](step05.md) - [6](step06.md) - [7](step07.md) - [8](step08.md) - [9](step09.md) - [10](step10.md) - [11](step11.md) - [**12**](step12.md) - End


# 課題6-2: モジュールに存在しない処理の冪等性を考える

shellモジュールは、使うと必ずchangedになってしまう（＝毎回実行されてしまう）という仕様があります。このモジュールは単にOSコマンドを実行するだけで、"コマンドを実行する必要があるか" や "変更を加えたか" の判断はしません。  
実行する必要のない状態で実行すると問題になる処理もあるため、処理内容に応じて冪等性を保つためのPlaybookを実装することが望ましい実装になります。  
本課題では、このような処理の有無を分岐させる方法について学んでもらいます。

## 1. Playbookの作成

`playbook_kadai-6-2.yaml`に以下をコピペします。

```yaml
---
- hosts: all
  roles:
    - kadai-6-2

```

## 2. タスクの作成

`exercise/02_basic/roles/kadai-6-2/tasks/main.yaml`に前課題の回答が記載されているため、このファイルに修正を加えて冪等性の考慮されたPlaybookにします。  
実装の要件は以下の通りです。

* 対象サーバのファイル`~/resultfile`にホスト名が出力されること
* 初回実行のみファイルが作成され、ログに`changed`が出力されること
* 2回目以降の実行ではファイルに変更を加えず、ログに`changed`が出力されないこと

* `hostname >> ~/resultfile`を実行するタスクは`skipping`になること
  * ヒント1: `register`という仕組みでタスクの実行結果を変数に保持できる
  * ヒント2: 変数内の要素の確認には`debug`モジュールが利用できる
  * ヒント3: 変数内の要素には`<変数名>.<要素名>`でアクセスできる
  * ヒント4: `ignore_errors: true`を付けると、そのタスクが正常終了しない場合も後続のタスクを実行できる
  * ヒント5: `changed_when: false`を付けると、そのタスクの実行結果は`changed`にならない

回答例は次のページに記載しています。  
本課題はこれまでのものより難易度が高く、実装の自由度も高いため、難しいと感じた場合は早々に見切りを付けて回答例を見てしまっても構いません。  
なお、冪等性を保つための方法はシェルコマンドの処理内容によっていろいろ考えられるため、特に明確な正解はありません。

## 3. Playbookを実行

以下の順番で実行してください。

以前の実行で作成された`resultfile`を削除

```bash
ssh target01 -i /root/.ssh/ansible_lesson_key "rm -f ~/resultfile"; \
ssh target02 -i /root/.ssh/ansible_lesson_key "rm -f ~/resultfile"
```

Playbookを実行

```bash
ansible-playbook -i inventory playbook_kadai-6-2.yaml
```

`resultfile`が作成されたことを確認

```bash
ssh target01 -i /root/.ssh/ansible_lesson_key "cat ~/resultfile"; \
ssh target02 -i /root/.ssh/ansible_lesson_key "cat ~/resultfile"
```

Playbookを再実行し、skippingになることを確認

```bash
ansible-playbook -i inventory playbook_kadai-6-2.yaml
```

`resultfile`に1行しかホスト名の記載された行が無いことを確認

```bash
ssh target01 -i /root/.ssh/ansible_lesson_key "cat ~/resultfile"; \
ssh target02 -i /root/.ssh/ansible_lesson_key "cat ~/resultfile"
```

---

- [前のページに戻る](step11a.md)
- [目次](README.md)
- [解説に進む](step12a.md)
