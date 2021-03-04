## 一、Git初期使用
### 1.1 命令总结
```java
1. git init                  // 初始化
2. git status  /*  检测状态 —— 分为三种： 
                              1.新增文件（红色）、
                              2.已使用git管理（绿色——>暂存区）、
                              3.生成版本（放入版本库）  */
3. git add File_Name         // 单独添加名为File_Name的文件
   git add .                 // 添加所有文件至暂存区
4. git commit -m '描述信息'   // 提交至版本库

//拓展功能
5. git log                   //查看git日志 使用q或退出
   git log --graph           //显示图形化日志
   git log --graph --pretty=format:"%h %s"  //日志简介版

6. git reset --hard + 版本号  //回滚至此前版本
7. git reflog                //查看包括回滚的日志
8. git reset --hard + 版本号  //撤销之前的某次回滚，回到此版本

git reset --soft 版本号       //撤销commit，回到暂存区
git reset head               //撤销add，回到工作区
git checkout -- +文件名       //撤销自动status
```

## 二、Git进阶
### 2.1 git 分支
  版本更改时，仅仅**更新所改变的文件**，没有改变的文件会**指向之前的版本**，以此类推。

适用于给使用者提供多个环境，可以把编码从主线上分离开来，以免影响开发主线。
```
C1 <- C2 <- C3
         <- C4   
```
### 2.2 分支管理命令总结
```
1. 查看分支
    git branch
2. 创建分支
    git branch +分支名称
3. 切换分支
    git checkout +分支名称
4. 合并分支（可能产生冲突）注意合并时需要切换主分支再合并
    git merge +要合并的分支
5. 删除分支
    git branch -d 分支名称
```
产生冲突后，可**手动处理冲突**，然后再按照流程重新添加

## 三、Github托管
### 3.1 github
1. 创建仓库
2. 获取仓库地址
3. **上传本地代码**

**(create a new repository on the command line)**
```
echo "# LastAndFound_weixin" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M master
git remote add origin https://github.com/chen934298133/Name.git
git push -u origin master
                
```

**(push an existing repository from the command line)**
```
git remote add origin https://github.com/chen934298133/Name.git
git branch -M master
git push -u origin master
```

4. **首次下载云端代码异地开发**

```
1. 克隆远程仓库代码
    git clone https://github.com/chen934298133/Name.git
2. 切换分支
    git checkout 分支
```

5. 给远程仓库**起别名**

```
1. 起别名
    git remote add Name https://github.com/chen934298133/Name.git
2. 向远程推送代码
    git push -u origin 分支
    git push origin 分支
```
6. 后续开发云端代码使用**pull**
```
1. pull 云端代码
    git pull origin 分支
2. 开发完毕后，按照上传流程重复命令
```
### 3.2 log 管理
1. rebase使用(注意尽量**不要**合并已经push上云端的log)
```
1. 合并多余log
    git rabase -i head~number
2. 处理完冲突，更新完成后，使用rebase continue
    git rebase --continue
```
2. Beyond Compare 解决冲突
    - 安装beyond compare
    - 在git中配置
      ```
      1. git config --local merge.tool bc3                // 合并工具起名为bc3
      2. git config --local mergetool.path '安装路径'      // 配置安装路径
      3. git config --lacal mergetoll.keepBackup false    // 保持更新        
      ```
    - 使用
      ```
      git mergetool
      ```
## 四、 多人协同开发
### 4.1 