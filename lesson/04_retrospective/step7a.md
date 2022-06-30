# 課題6: 条件分岐の使い方の応用

## 課題6-1: 実行確認用のタスクを作成する

taskのみ記載します。  
変数が未定義だとエラーになってしまうため、通常はどこかでデフォルト値を定義しておく必要がありますが、`when`の条件に`defined`を使うとコードを簡略化できます。

```yaml
- name: "ユーザ作成"
  user:
    name: "{{ item }}"
    state: present
  loop: "{{ users }}"
  when: users is defined

- name: "ユーザ確認コマンドの実行"
  shell: "tail -10 /etc/passwd"
  register: ret
  when: user_check is defined

- name: "ユーザ確認結果の出力"
  debug:
    msg: "{{ ret.stdout_lines }}"
  when: user_check is defined
```

表示する行数は適宜調整してください。`cat`でもよいです。  
なお、`block`を使うと以下のように`when`の条件文の記載を1つにまとめられます。  
複数のタスクをまとめて同じ条件で分岐させたい場合はこちらの方が記述ミスの可能性が少なくなり、可読性も良くなります。

```yaml
- name: "ユーザ作成"
  user:
    name: "{{ item }}"
    state: present
  loop: "{{ users }}"
  when: users is defined

- block:
  - name: "ユーザ確認コマンドの実行"
    shell: "tail -10 /etc/passwd"
    register: ret

  - name: "ユーザ確認結果の出力"
    debug:
      msg: "{{ ret.stdout_lines }}"

  when: user_check is defined
```

---

- [前のページに戻る](step7.md)
- [目次](README.md)
- [次のページに進む](step8.md)
