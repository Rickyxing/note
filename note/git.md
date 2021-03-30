

```
git使用
	git init(在该文件里创建一个git项目)
	git status 查看当前目录还有那些文件没有上传
	git add (上传一个文件到暂存区)
	git add . 名(点事所有文件,只上传到暂存区,版本库)
	git commit -m "更改信息" (放到版本库中)
		新功能:"feat:shopping"
		fix: "修改bug"
		docs:"文档"
		tmp: "临时提交"
	git diff "查看修改的内容"
	git log "查看修改信息"
  git log -p "所有的修改信息"
	git log --pretty=oneline "只看版本号"
  git reset --hard id
  git reset --hard HEAD^ "回到上一个版本,也可以回到删除的文件"
  git reflog "记录每一次命令"
  git restore --staged +本文件名 "在暂存区时撤销上传"
  git reset --soft HEAD^ "撤销commit后至上一次commit的版本"
  git rm 路径 "彻底删除文件"

	上传远程仓库
		拿到秘钥	$ ssh-keygen -t rsa -C "1335178212@qq.com"
		登陆GitHub，打开“Account settings”，“SSH Keys”页面：
		然后，点“New SSH Key”，填上任意Title，在Key文本框里粘贴`id_rsa.pub`
		
```

