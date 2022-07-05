# 課題5: 条件分岐を使用する

## 課題5-1: 変数が未定義の場合にタスクをSkipする

taskのみ記載します。

```yaml
- name: "ユーザ作成"
  user:
    name: "{{ item }}"
  loop: "{{ users }}"
  when: users is defined
```

---

- [前のページに戻る](step6.md)
- [目次](README.md)
- [次のページに進む](step7.md)

