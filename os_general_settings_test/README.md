# 実行方法

## プレイブック構造
```
os_general_settings_test/
├── README.md
├── inventory
│   └── inventory.ini
├── roles
│   └── common
│       ├── locale
│       │   ├── defaults
│       │   │   └── main.yaml
│       │   └── tasks
│       │       └── main.yaml
│       └── packages
│           ├── tasks
│           │   └── main.yaml
│           └── vars
│               ├── Debian.yaml
│               └── RedHat.yaml
└── setup.yaml
```

## プレイブック配置場所
- /etc/ansible/配下

## インベントリファイル
- `inventory/inventory.ini`
- 環境に応じてホスト名やIPアドレスを変えて下さい

## 環境
- ansibleコントロールノード
  - OSはAmazon Linux 2023
  - ansibleは2.15.13

- ansibleマネージドノード
  - OSはAmazon Linux 2023

## プレイブックの実行方法
```bash
$ cd /etc/ansible/os_general_settings_test`
$ ansible-playbook -i inventory/inventory.ini setup.yml`
```

## プレイブック解説
- パスは各ロールからの相対パスです。

- inventory/inventory.ini
ansible_hostはプレイブック実行時のターゲットノードIPアドレスです。

- localeロール
タイムゾーン、ロケール、キーボードを設定しています。
変数はlocale/defalts/main.ymlを参照しています。

- packagesロール
  - OSディストリビューションがDebianかRHELかで処理を変えています。
  - インストールされるパッケージは `vars/RedHat.yaml` と `vars/Debian.yaml` で定義しています。