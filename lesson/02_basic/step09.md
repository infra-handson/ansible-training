Start - [1](step01.md) - [2](step02.md) - [3](step03.md) - [4](step04.md) - [5](step05.md) - [6](step06.md) - [7](step07.md) - [8](step08.md) - [**9**](step09.md) - [10](step10.md) - [11](step11.md) - [12](step12.md) - End


# 条件分岐について

多少複雑なPlaybookや汎用的なPlaybookを作ると、変数やサーバの状態に応じて処理を分岐させたくなる場合が出てきます。  
例えばパッケージのインストールを考えてみましょう。  
パッケージをインストールするパッケージシステムはOSのディストリビューションによって`yum`や`apt`など異なるものが使われます。
Ansibleで実行させるタスクもディストリビューションによって使い分ける、といった場合に`when`を使って条件分岐させます。

Ansibleでは実行時に`ansible_os_family`というマジック変数が自動的に定義され、この値を参照するとOSのディストリビューションを識別することができます。  
`RedHat`系のOSは`yum`、`Debian`系のOSは`apt`を使ってパッケージのインストールを行うため、
これを利用して以下のようにコードを記述すると、どちらのOSに実行しても適切な方法でパッケージのインストールを行うPlaybookが作成できます。

```yaml
- name: "install Apache using yum"
  ansible.builtin.yum:
    name: httpd
    stat: present
  when: ansible_os_family == "RedHat"

- name: "Install Apache using apt"
  ansible.builtin.apt:
    name: apache2
    stat: present
  when: ansible_os_family == "Debian"
```

:warning:  
`when`では`ansible_os_family`のような変数を`{{}}`で囲わない点に注意してください。これはAnsibleのルールです。

実は`ansible.builtin.package`モジュールを使えばOSディストリビューションに応じて`dnf`、`apt`、`apk`など最適なパッケージシステムを切り替えて実行してくれます。  
ただし、上記の`httpd`と`apache2`のように同じソフトウェアでもパッケージ名がパッケージシステム毎に異なることがあり、こういった場合に`when`が必要になります。

---

- [前のページに戻る](step08a.md)
- [目次](README.md)
- [次のページに進む](step10.md)
