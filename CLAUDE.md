# CLAUDE.md

このリポジトリは macOS のセットアップを自動化する Ansible playbook。

## 作業サイクル

Ansible ロールの実装・変更を行う場合、必ず以下のサイクルで作業すること:

1. **実装** -- ロールを作成・編集する
2. **実行して検証** -- `ansible-playbook playbook.yml` を実行し、タスクが成功することを確認する
3. **再実行して冪等性を確認** -- もう一度実行し、`changed=0` になることを確認する

## ロールの構造

- ロールは `roles/<name>/tasks/main.yml` に配置する。既存ロールのパターンに従うこと。
- **Homebrew Cask アプリ** (`.app` をインストールするもの) は `stat` で既存チェック → `homebrew_cask` でインストールのパターンを使う:

```yaml
- name: Check if <App> is already installed
  stat:
    path: /Applications/<App>.app
  register: <app>_installed

- name: Install <App>
  community.general.homebrew_cask:
    name: <cask-name>
    state: present
  when: not <app>_installed.stat.exists
```

- **Homebrew formula** (CLI ツール) は `community.general.homebrew` で直接インストールする。`stat` チェックは不要:

```yaml
- name: Install <tool>
  community.general.homebrew:
    name: <formula-name>
    state: present
```

- **言語ランタイムやバージョン管理が必要なツール** (go, node, python など) は個別ロールを作らず `roles/mise` の `config.toml` にツールを追加する。mise がバージョン管理を担うため brew は使わない。
- タスク名は英語で「Check if ...」「Install ...」の形式にする。

## playbook.yml

新しいロールを追加したら `playbook.yml` の `roles` リストにも追加すること。忘れないこと。

## 「入れて」と言われたら

ツールやアプリを「入れて」「インストールして」と言われた場合、直接インストールするのではなく、Ansible ロールを作成して playbook に追加し、作業サイクルに従って実行・検証すること。

## 実行方法

```sh
ansible-playbook playbook.yml
```
