# 課題2-回答: Ansibleでファイルを配布する

`roles/kadai-2/tasks/main.yaml`

```yaml
---
- name: copy file
  ansible.builtin.copy:
    src: ./files/copy_file
    dest: /tmp/copy_file
```

`src`の相対パスの書き方には正解がいくつかあります。  
ベストプラクティスに準じたディレクトリ構成のため、copyモジュールで`scr`に指定したファイルを`files`フォルダから探してくれるので`scr`にはパスを省略して`copy_file`とだけ記載しても動作します。  
実際に動作確認をしてファイルが送られていることを確認してください。  

また、実行ログに`name`に記載した文字列が出力されること、既に当該ファイルが配置されている2回目以降の実行では`changed`ではなく`ok`(変更なし)になること を確認してください。

---

- [前のページに戻る](step04.md)
- [目次](README.md)
- [次のページに進む](step05.md)

