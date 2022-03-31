# Git Repo Sync

![license](https://img.shields.io/github/license/jauderho/git-repo-sync)

Git Repo Sync enables you to synchronize code to other code management platforms, such as GitLab, etc.

## Try Git Repo Sync

You can use the following example as a template to create a new file with any name under `.github/workflows/`.

```yaml
name: <action-name>

on: 
  - push
  - delete

permissions: read-all

jobs:
  sync:
    runs-on: ubuntu-latest
    name: Git Repo Sync
    steps:
    - uses: actions/checkout@v2
      with:
        fetch-depth: 0
        
    - uses: jauderho/git-repo-sync@63782025e80e84c48b25a1ee6bb9a22a3bd570d3
      with:
        # Such as https://github.com/wangchucheng/git-repo-sync.git
        target-url: <target-url>
        # Such as jauderho
        target-username: <target-username>
        # You can store token in your project's 'Setting > Secrets' and reference the name here. Such as ${{ secrets.ACCESS_TOKEN }}
        target-token: <target-token>
```

GitLab Example ([`.github/workflows/gitlabsync.yml`](https://github.com/jauderho/git-repo-sync/blob/main/.github/workflows/gitlabsync.yml))

```yaml
name: Gitlab Sync

on:
  push:
    branches:
    - main

permissions: read-all

jobs:
  sync:
    runs-on: ubuntu-20.04
    name: Git Repo Sync
    steps:      
    - uses: actions/checkout@a12a3943b4bdde767164f792f33f40b04645d846 # v2
      with:
        fetch-depth: 0
        
    - uses: jauderho/git-repo-sync@63782025e80e84c48b25a1ee6bb9a22a3bd570d3 # v0.1.0
      with:
        #target-url: ${{ secrets.GITLAB_URL }}
        target-url: https://gitlab.com/${{ github.repository }}.git
        # Such as jauderho
        #target-username: ${{ secrets.GITLAB_USERNAME }}
        target-username: ${{ github.actor }}
        # Create a PAT on gitlab.com and store it in GitHub Secrets as GITLAB_TOKEN
        target-token: ${{ secrets.GITLAB_TOKEN }}
```
