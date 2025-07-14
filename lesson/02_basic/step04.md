Start - [1](step01.md) - [2](step02.md) - [3](step03.md) - [**4**](step04.md) - [5](step05.md) - [6](step06.md) - [7](step07.md) - [8](step08.md) - [9](step09.md) - [10](step10.md) - [11](step11.md) - [12](step12.md) - End


# 課題2: Ansibleでファイルを配布する

本課題では、Ansibleの公式ドキュメントを参考にしながら自分で簡単なコードを作成する方法について学んでもらいます。  
題材として、copyモジュールを使ってファイル配置するPlaybookを作ります。  
※ファイル配置のイメージ  
![](img/arch_copy.drawio.svg)


## 1. Playbookの作成

`exercise/02_base/playbook_kadai-2.yaml`に以下をコピー＆ペーストします。

```yaml
---
- hosts: all
  roles:
    - kadai-2

```

## 2. ターゲットサーバへ配置するファイルの作成

`exercise/02_base/roles/kadai-2/files/copy_file`に以下をコピー＆ペーストします。

```text
ターゲットサーバに配置されるファイルです。
このサーバのホスト名は「target-server-01」です。
Ansible実行後にターゲットサーバに配置されていることを確認してください。

```

## 3. タスクの作成

[copyモジュールのドキュメント](https://docs.ansible.com/ansible-core/2.15_ja/collections/ansible/builtin/copy_module.html#ansible-collections-ansible-builtin-copy-module)を参考に、`exercise/02_base/roles/kadai-2/tasks/main.yaml`へタスクを作成します。  
実装の要件は以下の通りです。

* `copy`モジュールを使うこと
* 2で作成した`exercise/02_base/roles/kadai-2/files/copy_file`をターゲットサーバの`/tmp/copy_file`へ配置すること
  * 今回の場合は、`roles/kadai-2/`が相対パスの起点となる

回答例は次のページに記載していますが、どうしても上手くいかない場合にだけ参考にしてください。

## 4. Playbookを実行

```bash
ansible-playbook -i inventory playbook_kadai-2.yaml
```

## 5. 配置したファイルの確認

各ターゲットサーバへSSH接続し、`/tmp`ディレクトリに`copy_file`というファイルが配置されていることを確認します。  
以下のコマンドを1つ1つ実行していってください。

### 1号機

```bash
ssh target01 -i /root/.ssh/ansible_lesson_key
```

```bash
ls /tmp
cat /tmp/copy_file
exit
```

:warning:  
sshコマンドは引数にシェルコマンドを渡すと、リモート先でシェルコマンドを実行した結果が返ってきます。  
これを利用することで上記の確認操作を以下のように簡略化できます。  

```bash
ssh target01 -i /root/.ssh/ansible_lesson_key "cat /tmp/copy_file"
```

### 2号機

```bash
ssh target02 -i /root/.ssh/ansible_lesson_key
```

```bash
ls /tmp
cat /tmp/copy_file
exit
```

---

- [前のページに戻る](step03.md)
- [目次](README.md)
- [解説に進む](step04a.md)
