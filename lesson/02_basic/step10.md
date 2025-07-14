Start - [1](step01.md) - [2](step02.md) - [3](step03.md) - [4](step04.md) - [5](step05.md) - [6](step06.md) - [7](step07.md) - [8](step08.md) - [9](step09.md) - [**10**](step10.md) - [11](step11.md) - [12](step12.md) - End


# 課題5: 条件分岐を使う

本課題では、whenを使って特定の場合にだけ処理を実行するPlaybookを作る方法について学んでもらいます。  
題材として、特定の変数が定義されているターゲットにのみfetchを実行するPlaybookを作ります。

## 1. Playbookの作成

`playbook_kadai-5.yaml`に以下をコピペします。

```yaml
---
- hosts: all
  roles:
    - kadai-5

```

## 2. インベントリファイルに変数を定義

Step8で作成したインベントリファイルと同様の状態にしておいてください。

```yaml
all:
  hosts:
    target01:
      ansible_port: 2222
      ansible_user: hoge
      server_hostname: target-server-01  # 課題3で使用した変数
      fetch_files:
        - path: /etc/passwd
          dest: ./kadai-4_fetch_files_exp/foo
        - path: /etc/ssh/sshd_config
          dest: ./kadai-4_fetch_files_exp/bar
    target02:
      ansible_port: 2223
      ansible_user: foo
      server_hostname: target-server-02
      fetch_files:
        - path: /etc/group
          dest: ./kadai-4_fetch_files_exp/foo
        - path: /etc/profile
          dest: ./kadai-4_fetch_files_exp/bar
        - path: /proc/cpuinfo
          dest: ./kadai-4_fetch_files_exp/baz
  vars:
    ansible_ssh_private_key_file: ~/.ssh/ansible_lesson_key

```

## 3. タスクの作成

「[fetchモジュールのドキュメント](https://docs.ansible.com/ansible-core/2.15_ja/collections/ansible/builtin/fetch_module.html#ansible-collections-ansible-builtin-fetch-module)」と「[条件のドキュメント](https://docs.ansible.com/ansible-core/2.15_ja/playbook_guide/playbooks_conditionals.html#playbooks-conditionals)」を参考に、`exercise/02_basic/roles/kadai-5/tasks/main.yaml`へタスクを作成します。  
実装の要件は以下の通りです。

* `fetch`モジュールを使うこと
* `when`を使って、target01のサーバの`/etc/passwd`ファイルをだけを取得すること
  * target02からは取得しないこと。
  * インベントリを編集しないこと。
  * 何を条件にするかはお任せします。
* 取得したファイルはカレントディレクトリ直下の`kadai-5_fetch_files`というディレクトリに配置すること

回答例は次のページに記載していますが、どうしても上手くいかない場合にだけ参考にしてください。

## 4. Playbookを実行

```bash
ansible-playbook -i inventory playbook_kadai-5.yaml
```

target02への実行がskipになることを確認してください。

## 5. 取得したファイルの確認

Playbookを実行すると、カレントディレクトリ直下に`kadai-5_fetch_files`というディレクトリが表示されます。  
その中にtarget01から取得したファイルのみが入っていることを確認してください。  
なお、一度取得したファイルは自動で消えないため、コードを書き間違えてtarget02へ実行してしまった場合は再実行する前に手動で`kadai-5_fetch_files`ディレクトリを削除してください。

※ディレクトリが表示されない場合は、エディタ上の以下の位置にある更新ボタンを押してください。

![](img/refresh.png)

---

- [前のページに戻る](step09.md)
- [目次](README.md)
- [解説に進む](step10a.md)
