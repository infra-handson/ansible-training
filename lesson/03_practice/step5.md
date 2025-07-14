# Roleを使う

演習2-1で変数化を行いましたが、変数の値を変更したい場合は結局Roleディレクトリ内のファイルを書き換えていました。  
この運用ではRoleを使い回しにくいですし、実行対象ごとに異なる値を定義することができません。  
そこで、Ansibleにはサーバごとに変数を定義できるように`host_vars`と呼ばれる仕組みが存在しています。

![](img/role.drawio.svg)

## 演習3-1：host_varsを作成してRoleを実行する

host_varsは`host_vars`という名前のディレクトリを作成し、
その中にインベントリで記載している実行対象サーバと同じ名前のYamlファイルを作成することで行います。  
すでにファイルは作成済みなため、以下の手順でファイルを編集してください。

１. varsの値を元の状態に戻す

配置先ディレクトリを`/root`に変更しているかと思いますので、`/tmp`に戻します。  
`exercise/03_practice/roles/simple_role/vars/main.yaml`に以下をペーストして書き換えてください。

```yaml
---
dest_dir: "/tmp"

```

２. `target01`のhost_varsに変数を定義

`exercise/03_practice/host_vars/target01.yaml`に以下をペーストしてください。

```yaml
---
user_name: "Alice"

```

３. `target02`のhost_varsに変数を定義

`host_vars/target02.yaml`に以下をペーストしてください。  
こちらには`vars`に定義した変数と`defaults`に定義した変数の挙動の違いを確認するため、`dest_dir`も定義しておくことにします。

```yaml
---
dest_dir: "/opt"
user_name: "Bob"

```

４. Playbookの再実行

以下のコマンドでPlaybookを再実行します。

```bash
ansible-playbook -i inventory playbook_simple_role.yaml
```

今回もChangedになるはずです。

５. 実行確認

以下のコマンドで実行対象に配置されたファイルの内容を確認します。

```bash
ansible -m ansible.builtin.shell -a "cat /tmp/testfile" -i inventory all
```

以下のように出力されるはずです。  
サーバごとに異なる変数を定義して実行できていることが確認できます。  
また、`target02`の方は`dest_dir`に`/opt`を定義したにも関わらず、`vars`で定義している`/tmp`に配置されていることも確認できます。  
このように、変数化の目的に応じて`vars`と`defaults`を使い分けると実装の意図がわかりやすくなり、可読性が高くなります。

```text
target01 | CHANGED | rc=0 >>
My name is Alice.
target02 | CHANGED | rc=0 >>
My name is Bob.
```


⚠️補足  
Ansibleは`host_vars`以外にも変数を定義する方法が複数あります。  
よく使われるものだと、基礎編で使用していたインベントリでの定義、グループごとに変数を定義する`group_vars`があります。  
他も変数の定義方法、定義場所はありますが、同時に様々な場所に定義すると見通しが悪くなり保守管理しづらくなってしまいます。  
変数の詳細は[公式サイトの解説ページ](https://docs.ansible.com/ansible-core/2.15_ja/playbook_guide/playbooks_variables.html#playbooks-variables)を参照してください。

---

- [前のページに戻る](step4.md)
- [目次](README.md)
- [次のページに進む](step6.md)
