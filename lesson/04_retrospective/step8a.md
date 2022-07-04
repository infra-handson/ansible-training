# 課題7: 動作確認を行うPlaybook

## 課題7-1: 疎通確認を行うPlaybook

もっともシンプルだと思われる実装方法になります。  
`ping`が成功した宛先は`changed`になり、失敗した宛先は`failed`になります。

```yaml
- name: "疎通確認"
  shell: "ping -c 1 -W 1 {{ item }}"
  loop: "{{ ping_targets }}"
```

```yaml
# target01.yaml 記載例
ping_targets:
  - 172.18.0.3  # target02のIPアドレス（環境によって異なる）
  - 192.168.12.34  # 存在しないIPアドレス（failedになる）
  - localhost
  - 8.8.8.8  # Googleが提供しているパブリックDNSサービスのIPアドレス
```

```yaml
# target02.yaml 記載例
ping_targets:
  - 172.18.0.4  # target01のIPアドレス（環境によって異なる）
  - 8.8.8.8
```

実行結果は以下のようになります。

```text
TASK [common : 疎通確認] *************************************************************************************************************************************************************************************************************************************************************************************************
changed: [target02] => (item=172.18.0.4)
changed: [target01] => (item=172.18.0.3)
failed: [target01] (item=192.168.12.34) => {"ansible_loop_var": "item", "changed": true, "cmd": "ping -c 1 -W 1 192.168.12.34", "delta": "0:00:01.002984", "end": "2022-07-01 18:29:34.045496", "item": "192.168.12.34", "msg": "non-zero return code", "rc": 1, "start": "2022-07-01 18:29:33.042512", "stderr": "", "stderr_lines": [], "stdout": "PING 192.168.12.34 (192.168.12.34): 56 data bytes\n\n--- 192.168.12.34 ping statistics ---\n1 packets transmitted, 0 packets received, 100% packet loss", "stdout_lines": ["PING 192.168.12.34 (192.168.12.34): 56 data bytes", "", "--- 192.168.12.34 ping statistics ---", "1 packets transmitted, 0 packets received, 100% packet loss"]}
changed: [target01] => (item=localhost)
changed: [target01] => (item=8.8.8.8)
```

---

- [前のページに戻る](step8.md)
- [目次](README.md)
