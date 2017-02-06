## 分支说明
 1. master, 线上代码，稳定分支,发布到线上
 2. develop, 测试代码，最新分支,持续集成测试
 3. feature, 特性分支，开发新功能
 4. release, 预发布分支，防止线上环境出错的最后一道保证
 5. hotfix, BUG修复分支，修复线上BUG

## 流程说明
 1. 新需求，拉取一个 `feature` 分支
 2. 在 `feature` 分支开发自测
 3. 合并到 `develop` 分支(可自动化持续集成)，通知QA测试
 4. 如果测试通过，从 `master` 上拉取 `release` 分支, 将 `feature` 合并到 `release` 分支，然后对 `release` 分支测试( `release` 分支可能有多个 `feature`)；如果不通过，则返回第二步重新修复BUG
 5. 如果 `release` 分支通过测试，则 `merge request` 到 `matser` 分支，期间进行 `code review`；如果不通过，则返回第二步重新修复BUG
 6. 上线，如果线上没问题，则需求结束；否则，从 `master` 拉取 `hotfix` 分支进行BUG修复

## 流程图
 ![git workflow](http://oe8xfchya.bkt.clouddn.com/%E6%B5%81%E7%A8%8B%20%281%29.png)