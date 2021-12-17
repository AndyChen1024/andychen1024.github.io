# 新建博客


使用工具：[Hugo](https://gohugo.io/getting-started/quick-start/)

使用主题：[theme](https://hugoloveit.com/zh-cn/theme-documentation-basics/)

Git工具操作：新建github仓库，[用户名+github.io](http://xn--+github-6x3lv66hou3b.io)

进入本地blog相关的<font color = "red">public</font>文件夹，git init 并关联远程自己网页的库

```bash
# 在本地blog文件夹，使当前文件夹转为git库
git init
# 与自己的代码库关联
git remote add origin git@github.com:AndyChen1024/andychen1024.github.io.git
# 查看当前修改状态
git status
# 添加修改过得文件，  . 表示所有，也可以指定文件
git add .
# ""里面的内容就是提交内容的说明信息
git commit -m "init my blog"
# 关联相关的git分支
git branch --set-upstream-to=origin/master master
# 处理被拒绝push，把master库中没有的文件拉过来，主要是README.md
git pull --rebase origin master
# 提交代码
git push
# 或者
git push -u origin master
```



