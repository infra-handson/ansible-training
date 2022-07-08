# 課題1: アドホックコマンドを使う

## 課題1-1: 接続しているユーザ名の確認

target01サーバで接続ユーザ名を確認する。

```bash
ansible -m shell -a "whoami" -i inventory target01
```

以下のように出力されるはずです。

```bash
target01 | CHANGED | rc=0 >>
hoge
```

すべてのサーバで接続ユーザ名を確認する。

```bash
ansible -m shell -a "whoami" -i inventory all
```

以下のように出力されるはずです。  
※順序が逆になる場合もあり

```bash
target01 | CHANGED | rc=0 >>
hoge
target02 | CHANGED | rc=0 >>
foo
```

## 課題1-2: IPの確認

```bash
ansible -m shell -a "ip a" -i inventory all
```

`172.18.0.2`のようなIPアドレスがサーバのIPです。

## 課題1-3: ターゲットサーバ同士の疎通確認

**target01から**target02に`ping`を実行する。

```bash
# target02のIPアドレスが「172.18.0.2」だった場合
ansible -m shell -a "ping 172.18.0.2 -c 4" -i inventory target01
```

**target02から**target02に`ping`を実行する。

```bash
# target01のIPアドレスが「172.18.0.4」だった場合
ansible -m shell -a "ping 172.18.0.4 -c 4" -i inventory target02
```

## 発展課題: `ping`コマンドで`-c`オプションが必要な理由

アドホックコマンドはコマンドが終了するのを待ってからまとめてコマンドのリターン（実行結果）を返す仕様になっています。  
回数を指定しなかった場合の`ping`コマンドはコマンドが終了せずにずっと実行され続けるため、いつまでもコマンド実行完了待ちのまま止まってしまいます。  
`-c`オプションを指定すると指定の回数を実行したらコマンドが終了するようになります。

---

- [前のページに戻る](step2.md)
- [目次](README.md)
- [次のページに進む](step3.md)
