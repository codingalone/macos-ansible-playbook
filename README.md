# macOS Setup

新しい Mac を一発でセットアップする Ansible playbook。

## 実行

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)" \
  && eval "$(/opt/homebrew/bin/brew shellenv)" \
  && brew install ansible \
  && ansible-galaxy collection install community.general \
  && ansible-playbook playbook.yml
```
