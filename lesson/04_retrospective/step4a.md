# 課題3: ループを使用する

## 課題3-1: 複数のユーザを作成する

taskのみ記載します。

```yaml
---
- name: "ユーザ作成"
  ansible.builtin.user:
    name: "{{ item }}"
  loop:
    - nginx
    - docker
    - zabbix
    - postgres
```

## 課題3-2: 作成したユーザの確認

1ユーザずつ確認してもよいですが、今回は目視でまとめて確認したいので`/etc/passwd`の中身を見るのが手っ取り早いです。

```bash
ansible -m ansible.builtin.shell -a "tail /etc/passwd" -i inventory all
```

---

- [前のページに戻る](step4.md)
- [目次](README.md)
- [次のページに進む](step5.md)

