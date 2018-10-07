---


---

<h4 id="step-1-系统的安装">step 1 系统的安装</h4>
<p>推荐使用<a href="https://rufus.akeo.ie/?locale">rufus</a>作为系统启动盘制作工具，简单方便快捷，并且免费，常见的一套下一步下来，ubuntu 16.04之后驱动问题得到了有效的改善，相较于以往NVIDIA的手动安装驱动，系统的软件更新器更加的人性化<br>
<img src="https://upload-images.jianshu.io/upload_images/4253971-f8da61ee3c3d8e1e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240" alt="image.png"></p>
<h4 id="step-2-gnome的美化">step 2 Gnome的美化</h4>
<p>Ubuntu 18.04后正式弃用以往以来长期坚持的unity投向gnome的怀抱不得不说是个明智的选择，Gnome不管是主题的更改和界面的布局相较于unity都有明显的优点</p>
<h6 id="tap-1-gnome-tweak-tool的安装">tap 1 gnome-tweak-tool的安装</h6>
<pre><code>sudo apt install gnome-tweak-tool
</code></pre>
<p>Gnome-tewak-tool：<br>
<img src="https://upload-images.jianshu.io/upload_images/4253971-988b73dd2f81e3f3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240" alt="image.png"></p>
<blockquote>
<p>by the way Ubuntu更新后，已经不用强制使用apt-get命令而直接使用apt命令即可<br>
安装完成后，打开Ubuntu应用商店，下载以下几个基本的主题插件：<br>
user theme ：加载本地的shell主题<br>
hide top bar : ubuntu 18.04给每个应用新增了顶部标题栏，与系统顶部标题栏无法重叠，此插件的意义便在于此<br>
dash to dock : 用于移动dock栏于不同位置以及dock的一些常见配置<br>
主题、图标、字体保存目录分别对应为 /usr/share/themes  icons  fonts 或 ~/.themes  icons fonts<br>
推荐主题图标等下载地址：<a href="https://www.gnome-look.org/">gnome-look</a></p>
</blockquote>
<p><img src="https://upload-images.jianshu.io/upload_images/4253971-bacf98c56cc7d933.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240" alt="image.png"></p>
<h4 id="step-3-ssrpolipo">step 3 ssr+polipo</h4>
<p>@ssr安装之前，先准备好常用的命令，如git, python等，安装方式大同小异</p>
<pre><code>sudo apt install git // and so on
</code></pre>
<blockquote>
<p>由于Ubuntu 18.04是自带python3.6的，并且在笔者进行配置的时候在terminal直接输入python是提示未安装的，此时建议将python3.6的优先级改为最高，同时安装好pip3</p>
</blockquote>
<pre><code>sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.6.6 200
sudo apt install python3-pip
sudo pip3 install --upgrade pip
</code></pre>
<p>此时就可以开始配置ssr了</p>
<pre><code>sudo wget http://www.texfox.com/ssr
sudo mv ssr /usr/local/bin
sudo chmod 766 /usr/local/bin/ssr
ssr install
</code></pre>
<p>安装工作进行完毕之后当然下一步进行配置文件的修改</p>
<pre><code>ssr config
</code></pre>
<p>作为必填项目包括以下的几点：</p>
<pre><code>"server": ""
"server_port": 200,
"local_address": "127.0.0.1",
"local_port": 1080,
"password": "",
"method": "chacha20",
"protocol": "origin",
</code></pre>
<p>其他默认即可，服务器ip和密码通过vpn运营商或自己配置的vps获取，不做赘述<br>
之后的工作就是ssr的使用而已，终端输入ssr help，“你想要的，这里都有”<br>
<img src="https://upload-images.jianshu.io/upload_images/4253971-c2c06369cb0690f7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240" alt="image.png"></p>
<p>为了方便这里顺便列举出Chrome的安装以及<a href="https://github.com/FelisCatus/SwitchyOmega/releases">SwitchyOmega</a>的扩展程序加载</p>
<pre><code>sudo wget https://repo.fdzh.org/chrome/google-chrome.list -P /etc/apt/sources.list.d/  //添加下载源
wget -q -O - https://dl.google.com/linux/linux_signing_key.pub  | sudo apt-key add -  //公钥的导入
sudo apt-get update  //依赖更新
sudo apt-get install google-chrome-stable  //软件安装 
</code></pre>
<p>由于chrome现在已经禁止本地安装扩展程序，目前笔者试过的方法也较多，其中一个100%可以使用的方法为，以终端的方式运行，启动时添加如下依赖</p>
<pre><code>sudo google-chrome-stable --no-sandbox --enable-easy-off-store-extension-install 
</code></pre>
<p>这样启动虽然可以添加扩展程序，但是重新点击图标启动依旧然并卵= =<br>
最后的解决方案（不一定靠谱），打开Chrome之后，浏览器进入chrome://extension，打开开发者模式，刷新浏览器，再把crx插件拖拽进入，完工～！</p>
<p>实现浏览器上网后，下一步就是终端的连接了<br>
polipo的安装</p>
<pre><code>sudo apt-get install polipo    
</code></pre>
<p>编辑配置文件 etc/polipo/config</p>
<pre><code>socksParentProxy = "127.0.0.1:1080"
socksProxyType = socks5 
</code></pre>
<p>之后重启polipo即可</p>
<pre><code>sudo service polipo restart
</code></pre>
<h4 id="step-4-deepin-wine">step 4 deepin-wine</h4>
<p>不得不说<a href="https://github.com/wszqkzqk/deepin-wine-ubuntu">deepin-wine</a>确实是目前接触linux以来用的最舒服的一个，进入连接下载或clone安装包到本地，解压后运行./install.sh安装即可<br>
详细的容器等信息在github主页readme文件有详细列表，这边列举大家比较关注的两个<a href="http://mirrors.aliyun.com/deepin/pool/non-free/d/deepin.com.qq.im/deepin.com.qq.im_8.9.19983deepin23_i386.deb">qq</a>、<a href="http://mirrors.aliyun.com/deepin/pool/non-free/d/deepin.com.wechat/deepin.com.wechat_2.6.2.31deepin0_i386.deb">微信</a> TIM这边测试无法发送和接收图片，详细未去深究，已经够用了不是<br>
<img src="https://upload-images.jianshu.io/upload_images/4253971-b4206a6a2809b1d8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240" alt="image.png"></p>
<p>值得一提的是这个并非网页版微信的提取，而是pc版，可以加载历史记录等，点个赞</p>
<h4 id="step-5-alert">step 5 alert</h4>
<p>alert是Ubuntu 18.04中比较喜爱的一个功能，添加方法稍显麻烦，如下</p>
<pre><code>wget -nv -O Release.key https://build.opensuse.org/projects/home:manuelschneid3r/public_key
sudo apt-key add - &lt; Release.key
sudo apt update
sudo sh -c "echo 'deb http://download.opensuse.org/repositories/home:/manuelschneid3r/xUbuntu_18.04/ /' &gt; /etc/apt/sources.list.d/home:manuelschneid3r.list"
sudo apt update
sudo apt install albert
</code></pre>
<p><img src="https://upload-images.jianshu.io/upload_images/4253971-381a17e1a00ffd56.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240" alt="image.png"></p>
<h4 id="the-end">the end</h4>

