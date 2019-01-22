# vue-props
vue 父子组件的双向数据绑定

__运行项目__

vue serve props.vue

## 上传项目到github 步骤

* 在本地项目文件夹中，右键 __`git bash here`__ 进入git

* __`git init`__ 进行初始化
* 验证SSH是否配置成功 __`ssh -T git@github.com`__ (如果提示The authenticity of host 'github.com (192.00.222.222)' can't be established.RSA key fingerprint is SHA256:xxxxx.Are you sure you want to continue connecting (yes/no)? 这是第一次的警告 输入yes会提示 You've successfully authenticated, but GitHub does not provide shell access.
代表成功！）

* 本地仓库与远程仓库关联 __`git remote add origin  git@github.com:hyq11/vue-props.git`__

* __`git add .`__ (.代表一次性添加所有文件)

* __`git commit -m "提交说明"`__

* __`git clone git@github.com:hyq11/vue-props.git`____ (克隆到本地仓库，入服务器上是空的，跳过此步)

* __`git remote add origin git@github.com:hyq11/vue-props.git`__ (添加后，远程库的名字就是origin，这是Git默认的叫法，也可以改成别的，但是origin这个名字一看就知道是远程库)

* __`git push -u origin master`__ (把本地内容推送到远程) 。

______

others：__`ls -al`__ 查看你的文件目录

* __`git branch`__  查看有哪些分支 git branch my 创建一个名为my的分支

* __`git checkout my`__  切换到my分支

* __`git merge`__  合并操作

* __`git branch -D my`__  删除my分支

* __`git fetch origin master`__  将服务器代码（不会合并到任何分支）git merge 合并到主分支

* __`git pull origin master`__  相当于fetch 和 merge 一起执行了


商业转载请联系作者获得授权，非商业转载请注明出处。
