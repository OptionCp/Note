---


---

<h3 id="git操作记录">git操作记录</h3>
<ul>
<li>sshkey的获取
<ul>
<li>Windows
<ul>
<li>打开git bash 输入
<blockquote>
<p>ssh-keygen -t rsa -C <a href="mailto:%22email@example.com">"email@example.com</a>"</p>
</blockquote>
</li>
<li>生成的sshkey保存位置为：~./.ssh/id_rsa中</li>
<li>复制sshkey保存于GitHub对应位置</li>
<li>绑定用户名与邮箱</li>
</ul>
<blockquote>
<p>git config --global <a href="http://user.name">user.name</a> “username”<br>
git config --global user.email “email”<br>
global 意为全局</p>
</blockquote>
</li>
</ul>
</li>
<li>基本操作
<ul>
<li>git init 初始化本地仓库位置</li>
<li>git clone <a href="mailto:git@github.com">git@github.com</a>:usrname/project.git 拷贝云端文件</li>
<li>git add .  添加目录下所有文件</li>
<li>git add --update</li>
<li>git commit -am “Remark”</li>
<li>git push -u origin master</li>
</ul>
</li>
</ul>

