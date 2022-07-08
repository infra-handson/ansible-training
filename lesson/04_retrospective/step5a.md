# 課題4: 変数を使用する

## 課題4-1: 変数で任意のユーザを作成できるようにする

taskの他、`host_vars`ディレクトリの`target01.yaml`と`target02.yaml`も編集が必要です。

```yaml
# task
- name: "ユーザ作成"
  user:
    name: "{{ item }}"
  loop: "{{ users }}"
```

```yaml
# target01.yaml 記載例
users:
  - taro
  - jiro
```

```yaml
# target02.yaml 記載例
users:
  - alice
  - bob
```

## 課題4-2: 作成したユーザの確認

```bash
ansible -m shell -a "tail -10 /etc/passwd" -i inventory all
```

表示する行数は適宜調整してください。`cat`でもよいです。

---

- [前のページに戻る](step5.md)
- [目次](README.md)
- [次のページに進む](step6.md)
