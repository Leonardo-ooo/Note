Git Note

```c
git config --global user.name "Your Name"		//设置用户名
git config --global user.email "email@example.com"	//设置邮箱
git init	//初始化当前文件夹，记录文件夹的更改
git add file_name		//添加文件到仓库缓存区
git commit -m "更改内容描述"	//将缓存区所有文件提交到仓库
git log		//查看版本情况
git status	//查看文件修改情况
git diff	//查看具体修改内容
git reset --hard HEAD^ 	//回到上一个版本  HEAD^^上两个版本，HEAD~n上n个版本
git reflog	//查看历史版本id即描述（用于寻找未来版本的id）
ssh-keygen -t rsa -C "youremail@example.com"	//创建ssh key
git push -u origin master	//把本地库的所有内容推送到远程库上
```

