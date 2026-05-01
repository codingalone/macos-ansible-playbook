# macOS Setup

新しい Mac を一発でセットアップする Ansible playbook。

## 実行

まず Xcode Command Line Tools を入れる (git などが使えるようになる):

```bash
xcode-select --install
```

次にリポジトリを clone して playbook を流す:

```bash
git clone https://github.com/codingalone/macos-ansible-playbook.git ~/dev/ansible \
  && cd ~/dev/ansible \
  && /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)" \
  && eval "$(/opt/homebrew/bin/brew shellenv)" \
  && brew install ansible \
  && ansible-galaxy collection install community.general \
  && ansible-playbook playbook.yml
```

playbook 実行時に macOS の sudo パスワードを聞かれる。`.pkg` 形式の cask (karabiner-elements / displaylink / google-japanese-ime / google-drive 等) のインストールには sudo が必要なため。

## App Store のアプリについて

`mas` 経由でインストールする App Store アプリ (Xcode / Dato / Bitwarden など) は、初回だけ App Store GUI から「入手」 (Get) を押しておくか、または既に当該アプリを購入/入手済みの Apple ID でログインしておく必要がある。`mas` は acquire (購入/入手) は出来ず、既に Apple ID に紐付いたアプリの install しか出来ないため。
