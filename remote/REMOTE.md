## Remote 節點

遠端儲存庫節點，可以是 GitHub, GitLab, BitBucket

常用指令

```bash
git remote -v
```

顯示如下，表示使用 ssh 方式 clone 專案，關於 SSH 介紹可以參考 [SSH.md](./SSH.md)

```bash
origin  git@github.com:Luca-Lin/git-practice.git (fetch)
origin  git@github.com:Luca-Lin/git-practice.git (push)
```

顯示如下，表示使用 HTTPS 方式 clone 專案

```bash
origin	https://github.com/Luca-Lin/git-practice.git (fetch)
origin	https://github.com/Luca-Lin/git-practice.git (push)
```

## 更改 Remote 的值

當從 Remote 使用 HTTPS Clone 專案想更改為使用 SSH 方式的話，不用重新 clone 一次。

只需要將 remote 名為 origin 的 value 改為 ssh 的 URL 即可。

```bash
git remote set-url origin git@github.com:Luca-Lin/git-practice.git
```

## 增加 Remote 的數量

情境

1. 當你這份專案要推到兩個 remote 的時候
2. 你是 fork 別人的專案後，clone fork 的專案時，想要獲取原本專案的進度

以上情境參考用，如果你要弄兩個名字不一樣但 url 是一樣的也是可以拉。

命名習慣，通常 fork 過後的專案，會叫下游 (downstream)，原本的專案會叫上游（upstream）

你可以依照這個方式添加一個 remote，當然你也可以隨便取 XD

```bash
git remote add upstream https://github.com/monosparta/git-practice
```

這樣子就增加一個 remote 了

```bash
origin  git@github.com:Luca-Lin/git-practice.git (fetch)
origin  git@github.com:Luca-Lin/git-practice.git (push)
upstream        https://github.com/monosparta/git-practice (fetch)
upstream        https://github.com/monosparta/git-practice (push)
```
