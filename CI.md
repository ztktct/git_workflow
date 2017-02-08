# 持续集成实践（Jenkins + Gitlab）

## 自动化需求
 1. 测试环境代码持续集成，自动化编译，打包，发布 (考虑自动化测试：单元测试、功能测试等)
 2. 线上环境自动化编译，打包，发布

## Jenkins 功能
 1. 关联 gitlab, 当 相关分支 有代码改动时，自动构建并发布
 2. 构建成功或失败后邮件推送

## 搭建jenkins、gitlab环境
 #### [Gitlab](http://blog.csdn.net/discoverer100/article/details/51814171)
 #### [Jenkins](http://blog.csdn.net/fenglailea/article/details/26014685/)
 
 ```
    Gitlab plugin、Gitlab Hook Plugin、Git plugin、Email Extension plugin
 ```

# 以下以项目 vue-jdly 为例
 ### 项目地址：[https://github.com/ztktct/vue-jdly](https://github.com/ztktct/vue-jdly)
 ### 流程参照：[git workflow](https://github.com/ztktct/git_workflow/blob/master/README.md)

 ## 项目操作步骤(默认已搭建jenkins、gitlab)
  ### 项目初始化
        1. Gitlab 创建项目
        2. 项目首次初始化、运行、编译、发布
  
  ### 在 Jenkins 创建 Job
        1. 源码管理，允许 Jenkins 从Gitlab获取源码
        2. 构建触发器 Build when a change is pushed to GitLab
        3. 自定义构建命令
            * npm run build
            * SFTP / npm run publish =====
        4. 构建后发送邮件通知
