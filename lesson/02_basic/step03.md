Start - [1](step01.md) - [2](step02.md) - [**3**](step03.md) - [4](step04.md) - [5](step05.md) - [6](step06.md) - [7](step07.md) - [8](step08.md) - [9](step09.md) - [10](step10.md) - [11](step11.md) - [12](step12.md) - End


# Ansible公式ドキュメントの見方を知る

Ansibleは公式ドキュメントが充実しており、頻繁にバージョンアップをされることからも、
コーディング時は基本的に公式ドキュメントを参考にすることになります。  
ここでは主にどのような内容が記載されていて、何を参考にコーディングすればよいのかを説明します。

なお、本トレーニング環境はAnsible Core 2.15で構成しているため、公式ドキュメントは2.15のドキュメントを見るようにしてください。  
インターネット上の情報を参考にする際も、なるべく2.15の情報かどうかを意識するようにしてください。

Ansible Core 2.15公式ドキュメント  
[https://docs.ansible.com/ansible-core/2.15_ja/index.html](https://docs.ansible.com/ansible-core/2.15_ja/index.html)


## モジュールのドキュメントを見る

Ansibleでのコーディングをする際にもっとも参照するのがモジュールのページになります。  
全モジュールのリストはバージョンごとに異なるため、`latest`ではなく使用するバージョンのページを参照してください。  
サイドメニューから辿っていくこともできますが、以下のリンクから直接アクセスしてもよいです。  
このリストの中から使えそうなモジュールを探していくことになります。  
[https://docs.ansible.com/ansible-core/2.15_ja/collections/ansible/builtin/index.html#plugins-in-ansible-builtin](https://docs.ansible.com/ansible-core/2.15_ja/collections/ansible/builtin/index.html#plugins-in-ansible-builtin)

今回は課題1で使用したFetchモジュールのページを見ていくことにします。  
上記ページのModulesから「[fetch module](https://docs.ansible.com/ansible-core/2.15_ja/collections/ansible/builtin/fetch_module.html#ansible-collections-ansible-builtin-fetch-module)」と遷移してください。  
なお、今回のように使用したいモジュール名が事前に明確な場合はGoogle等の検索エンジンサイトで「Ansible fetch」のように検索すると手っ取り早いです。

## モジュールページの見方について

各モジュールのページには主にパラメータとサンプルコードが記載されています。  
ここで最低限確認すべきことは、`required`と記載されているパラメータの意味と指定方法になります。  
その他のパラメータに関しては目的に応じて意味や使い方を確認してください。

例えばfetchモジュールの場合はサンプルコードを見ると以下のような記載があります。

```yaml
- name: Store file into /tmp/fetched/host.example.com/tmp/somefile
  ansible.builtin.fetch:
    src: /tmp/somefile
    dest: /tmp/fetched
```

パラメータの説明では、
`src`は取得対象のファイルパスを指定するパラメータ、`dest`は取得したファイルをAnsible実行サーバのどのディレクトリに配置するのかを指定するパラメータであることが記載されているため、
上記サンプルは実行対象の`/tmp/somefile`ファイルを`/tmp/fetched`ディレクトリに取得するコードだと読み取れます。  
そのため、上記サンプル通りにコードを記載して`src`と`dest`の値を適切に書き換えればコーディングが完了します。  
なお、`name`はどんなタスクなのかを説明するためのパラメータで、任意の文字列を指定することが可能です。実行ログに出力される文字列なので指定しましょう。
`name`はモジュールのパラメータではないため、インデントの深さに注意してください。

## コレクションについて

コレクションとはモジュールをまとめたものです。プログラム言語に例えると、モジュールが関数、コレクションがライブラリに相当します。
本環境では、ansible-coreに含まれる`ansible.builtin`というLinuxの基本操作をカバーするコレクションがインストールされています。
Windowsやネットワーク機器、クラウドサービスなど、Ansibleで操作する対象を増やすにはコレクションを追加します。  
代表的なコレクションは[Collection Index](https://docs.ansible.com/ansible/latest/collections/index.html)で公開されています。
また、有志が作成したコレクションが[ansible-galaxy](https://galaxy.ansible.com/)でも公開されていますが、動作やセキュリティ（悪意ある可能性もある）の品質が玉石混交なので、こちらの利用には注意が必要です。

---

- [前のページに戻る](step02.md)
- [目次](README.md)
- [次のページに進む](step04.md)
