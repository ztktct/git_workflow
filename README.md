## 分支说明
 1. master, 线上代码，稳定分支,发布到线上
 2. develop, 测试代码，最新分支,持续集成测试
 3. feature, 特性分支，开发新功能
 4. release, 预发布分支，防止线上环境出错的最后一道保证，预发布环境
 5. hotfix, BUG修复分支，修复线上BUG

## 当前流程
 1. 新需求，从 `develop` 拉取一个 `feature` 分支
 2. 在 `feature` 分支开发自测
 3. 修改 `package.json` 版本号，合并回 `develop` 发布测试
 4. 测试通过，从 `master` 拉取 `release` 分支， `cherry-pick` feature 的 commits 到 release
 5. 提交 `merge request`，期间进行 `code review`
 6. 上线，如果线上没问题，则需求结束；否则，从 `master` 拉取 `hotfix` 分支进行BUG修复，合回 `master` 和 `develop`

```
   存在问题：
     1. 从 `develop` 分支拉取，可能会包含其他feature,当前分之不干净
     2. 测试环境，当有多个功能测试，需要手动切换版本号以对应功能， `develop` 是否需要版本对应？
     3. 测试通过后，需要手动 'cherry pick' 一条条 commit 到 `release`, 中间浪费大量时间，而且可能漏掉一些 commit
```

## 新流程说明
 1. 新需求，从 `master` 拉取一个 `feature` 分支
 2. 在 `feature` 分支开发自测
 3. 合并到 `develop` 分支，通知QA测试
 4. 如果测试通过，从 `master` 上拉取 `release` 分支, 将 `feature` 合并到 `release` 分支，然后对 `release` 分支测试( `release` 分支可能有多个 `feature`)；如果不通过，则返回第二步重新修复BUG
 5. 如果 `release` 分支通过测试，则 `merge request` 到 `matser` 分支，期间进行 `code review`；如果不通过，则返回第二步重新修复BUG
 6. 上线，如果线上没问题，则需求结束；否则，从 `master` 拉取 `hotfix` 分支进行BUG修复，合回 `master` 和 `develop`

```
   解决问题：
      1. 从 `master` 稳定代码上拉取，保证新分支干净
      2. 把 `develop` 当做测试环境，测试环境将会包含所有新功能，可以同时测试多个功能而无需手动切换版本号
      3. 测试通过，正常情况下可以直接把将要上线的 `feature` 合并到 `release`,而无需 `cherry pick`
```

## 流程图
 ![git workflow](http://oe8xfchya.bkt.clouddn.com/%E6%B5%81%E7%A8%8B%20%282%29.png)

## 关于自动化
 1. `feature` 合并到 `develop` 上时，`develop` 自动编译、打包、发布测试
 2. `master` 代码更新后自动打TAG,发版本
 3. 项目代码发布成功后自动邮件提醒成功/失败

### 待讨论
 1. 是否需要 `release` 预发布环境？
 2. 我只是改个小功能，一些文案也需要按流程来？
 3. `code review` 时机