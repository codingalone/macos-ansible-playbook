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
