这边文档介绍了Seeed文档系统以及如何写或者修改一篇文档。因为这次只是修改文档，文章里有一些内容这次暂时用不上，要等以后要你们要从头写一篇新文档以及自己上传到文档系统才需要看，我都标注出来了。

## 主要步骤
如果是写一篇新文档并且上传到系统，主要步骤如下：

- 安装Mkdocs
- 将Seeed-WiKi文件夹拷贝到本地
- 如果是写一篇新文档，在Github创建Seeed-Document仓库里创建子仓库
- 把创建好仓库拷贝到本地
- 在把文档以及图片和其他资源托管在Github仓库
- 用Markdown编辑器编写文档
- 将新的文档放到Seeed-WiKi仓库的Docs文件夹
- 通过Bash build.sh生成site文件
- 把site文件上传到AWS S3

这次是修改文档，所以步骤简化为

- 安装Mkdocs
- 让聪哥给你的账户开github里Seeed_Document的权限
- 将那三篇文档在github的仓库拷贝到本地
- 用Markdown编辑器修改文档
- 将修改后的文档重新上传到github

## 前期准备
### 安装Mkdocs：
Mkdocs是用Python写的，所以也要用Python来安装。主要有三个步骤。
1．	安装Python
2．	安装Pip，如果Python版本比较高，可能已经带了Pip，可以通过以下命令查询是否已经安装。
```
$ python --version
Python 2.7.2
$ pip --version
pip 1.5.2
```
3．	安装Mkdocs
运行 mkdocs help 以检查是否正确安装.
```
$ mkdocs help
mkdocs [help|new|build|serve|gh-deploy] {options}
```
具体怎么安装可以参考以下两个链接。
- Mkdocs官网中文文档：[http://markdown-docs-zh.readthedocs.io/zh_CN/latest/](http://markdown-docs-zh.readthedocs.io/zh_CN/latest/)
- 这个博客写的安装方法更为详细：[http://blog.csdn.net/kevindgk/article/details/52388542](http://blog.csdn.net/kevindgk/article/details/52388542)

### 把Seeed-WiKi仓库拷贝到本地。
>因为暂时还不需要你们上传新文档到wiki.seeed.cc. 这个步骤可以暂时忽略

安装好Mkdocs以后，第一件事是先把Github上SeeedDocument下面Seeed-WiKi仓库拷贝到本地。步骤如下：
- 首先你需要注册一个github的账号，然后让把账号给聪哥，让聪哥给你Seeed-WiKi的权限。
- 在你想要存放Seeed-WiKi的硬盘里，鼠标右键，选择**bash**.
通过以下命令把Seeed-Wiki整个仓库的内容拷贝到本地。
```
git clone https://github.com/SeeedDocument/Seeed-WiKi
```
- 打开Seeed-WiKi的文件夹，你可以看到如下的内容

 [Seeed-WiKi文件夹的截图]

其中**Docs**用于存放所有我们想要在网页上显示的文档的Markdown文件。以后每次新写的Markdown文件，都要放到这个Docs文件夹里。

将Seeed-WiKi拷贝下来之后，我们先不用管他。下面我们开始说怎么写一篇具体的文档。

## 写文档
下面会详细说如何写一篇具体的文档，我们以Wifi Shield v1.0这个文档来做个例子。写之前，我们还需要做一些事情：

>1,2,3,4这次暂时可以忽略，直接看5

1.	在github建立该文档的仓库。文档以及和文档相关的资料都会储存在那里。

![](https://github.com/SeeedDocument/Tutorial_for_Bill/raw/master/res/%E5%88%9B%E5%BB%BAgithub%E4%BB%93%E5%BA%93.png)

2.	将仓库拷贝到本地。（方法同拷贝Seeed-Wiki的仓库，只是链接要换成你新建立的这个仓库的链接）。我们创建的仓库的链接是https://github.com/SeeedDocument/Wifi_Shield_v1.0，所以
```
git clone https://github.com/SeeedDocument/Wifi_Shield_v1.0
```
3.	拷贝到本地后，在该仓库中创建两个文件夹命名为img和res。其中 img用于存放图片，res用于存放图纸等其他资源，
4.	在仓库中右击鼠标，选择打开bash，用以下命令将包含有图片和资源的文档重新上传到github。
```
git add .
```
```
git commit –m”这里输入你更新了什么，我一般就直接写update”
```
```
git push origin master
```
这时候会让你输入github的账户名和密码。输密码的时候不会显示出来，直接输完按回车就可以了。等上传之后，刷新github的仓库链接，就可以看到多了两个文件夹。

5. 上面是写一篇新文档的步骤，这次只是修改文档，所以你们在Seeed_Document里面找到那几篇文档的仓库，再用"git clone"拷贝下来就可以了。
```
git clone 文档在github的链接
```
将文档拷贝到本地后，你就可以用Markdown编辑器将文档打开了，我软件用的那个叫}Atom"，配合在线编辑器[马克飞象](https://maxiang.io/#)很多人会用Markdown Pad, 具体要看你的电脑是什么操作系统。下面这篇文章介绍的很全面，你可以根据自己的需求和实际情况选一个合适的编辑器。
- [好用的Markdown编辑器一览](http://www.williamlong.info/archives/4319.html)

至于Markdown的介绍，可以参考这里：：[认识与入门Markdown](http://sspai.com/25137)。或者通过别搜索引擎了解更多关于Markdown的知识。这些都不是很难，很快就可以上手。

我们经常要用到的有以下几个语法：

<big>**1.标题**</big>
---
```
# 这是一级标题
## 这是二级标题
### 这是三级标题
```
<big>**2.链接**</big>
---
```
[要加超链接的文字](超链接)
```
<big>**3.图片**</big>
---
```
![图片名](超链接)
```
<big>**4.表格**</big>
---
```
|表头|表头|表头|
|---|---|---|
|内容|内容|内容|
|内容|内容|内容|
```
内容可以是文字，也可以是图片

<big>**5.列表**</big>
---
```
- 这是一级列表
- 这是一级列表
- 这是一级列表
 - 这是二级列表
 - 这是二级列表
  - 这是三级列表
  - 这是三级列表
```

接下来就是具体怎么写一篇文档了。

**开头添加的固定内容. **

如果你打开Docs文件夹里任何一篇Markdown文件，你会发现每篇文档开头都有类似下面这种的固定内容。这次因为是修改文档，这些固定内容已经有了，以后如果要写新文档，这些内容是必须要添加的。

```
---
title: G1/8" Water Flow Sensor(文档的标题)
category: MakerPro（文档所在的目录分类）
bzurl: https://www.seeedstudio.com/Wifi-Shield-p-1220.html（文档在Bazzar的商详页面链接）
oldwikiname:  G1/8" Water Flow Sensor（这个可以不用管，是移植稳当的时候用的。）
prodimagename:  phoint1.jpg（第一张图片的名称）
surveyurl: https://www.research.net/r/G1-8_Water_Flow_Sensor（问卷调查的链接，这个下面会说怎么生成）
sku:   113030003（产品的sku）
---
```
添加这些内容主要的目的是只通过一句指令，可以将文档编译成site文件的同时，在yml目录文件里自动添加该文档的信息。指令是：
```
bash build.sh
```
这个步骤和mkdocs官网说的使用"Mkdocs build"指令生成site文件有点不一样。因为"bash build.sh" 执行后么会自动执行“mkdocs build"指令。由于第一次使用，上面这一段解释你可能会看不懂，不过没关系，指令你也暂时用不上，你只要知道在文当前加那一段固定内容很重要就可以了。

**问卷调查**

>这次你们不用生成新的问卷调查，这里也可以忽略。但是如果以后要生成问卷调查，可以参考这里。

这里要特别说一下问卷调查，每篇稳当的末尾都会有一篇问卷调查用来调查用户的使用反馈。这些问卷调查时在网站Survey Monkey生成的。针对每一篇文档，我们都需要去Survey Monkey生成一个新的问卷调查。然后把生成的那个连接填在刚才那个固定内容里。这样编译的时候，就会自动在文档的末尾加上问卷调查了。下面介绍一下怎么生成问卷调查的链接。

- 首先登陆Survey Monkey的网站，因为这次不用生成问卷，账号密码我就先不写在这里了。
- 登陆之后，应该可以看到下面这个界面，选"Create Survey"
![](https://github.com/SeeedDocument/Tutorial_for_Bill/raw/master/res/Create%20Survey.png)

- 选择“Copy existing survey”

![](https://github.com/SeeedDocument/Tutorial_for_Bill/raw/master/res/Copy%20existing%20survey.png)

- 这时候会出现一些Survey让你选择，每次出现的都不一样，你随便选一个就可以了。我这次选的是Grove - Base Shield for IOIO-OTG
- 选择“Copy Survey“
![](https://github.com/SeeedDocument/Tutorial_for_Bill/raw/master/res/copy%20survey.png)

- 因为是Copy过来的，所以要改一下标题。把鼠标移到标题的区域，会出现“Edit”的字样，选择“Edit”。然后改成新的文档的标题。
![](https://github.com/SeeedDocument/Tutorial_for_Bill/raw/master/res/Edit.png)

- 改完标题后，选择“Next”

![](https://github.com/SeeedDocument/Tutorial_for_Bill/raw/master/res/next.png)

- 选择“Get Web Link”
- 选择“Customize”修改Survey的链接，把后缀修改成产品的名字
![](https://github.com/SeeedDocument/Tutorial_for_Bill/raw/master/res/Customize%201.png)
![](https://github.com/SeeedDocument/Tutorial_for_Bill/raw/master/res/customize-2.png)
- 选择“Show advanced Options” ，下面会增加一些额外的选项

![](https://github.com/SeeedDocument/Tutorial_for_Bill/raw/master/res/show%20advance%20options.png)

- 选择“Survey End Page”，然后在三个选项中选中间那个，填上这个链接：http://wiki.seeed.cc/survey_end/。这个步骤的作用是让用户填完Survey 之后能显示我们自己定义的内容，而不是Survey Monkey的广告。
![](https://github.com/SeeedDocument/Tutorial_for_Bill/raw/master/res/Survey%20end%20page.png)

- 然后再把最上面那个刚才修改过的Survey的链接Copy一下就可以了。
![](https://github.com/SeeedDocument/Tutorial_for_Bill/raw/master/res/Survey%E7%9A%84%E9%93%BE%E6%8E%A5.png)

步骤二：加了这些内容以后，就可以写文档的正文了 ，一般一篇文档会包含以下内容。

- Introduction 产品描述， 一般会配一张到两张图片，介绍完后在末尾加上“Get One Now”的Icon。（需要注意的是，如果文档添加了刚才介绍的那些固定内容，那就不用加## Introduction的标题了，编译的时候会自动生成。）
- Features  产品特性， 用列表或者表格的形式
- Specifications  产品参数， 用列表或者表格的形式
- Application Ideas  应用的点子， 列表或者表格的形式。重点产品的要加图片以及连接到具体的网页。
- Hardware Overview  产品硬件介绍， 配图片以及表格
- Getting Started 介绍产品具体怎么使用
- Resources  产品的图纸，datasheet等资料以及外部连接。

有时候针对重点产品也会加FAQ的板块，FAQ里并不是真的可以问问题，而是我们罗列一些常见的问题并在下面写出解答。

!!!Note
    这些标题都属于二级标题，一般要在前面加两个“#”号。比如：## Introduction。

目前大部分的产品都会包含这些板块，有些比较简单的产品可能会删去一些，或者一些复杂的产品会有额外板块，这里我们就不多介绍了。

按照这些板块写完文档之后，将文档保存到相应的文件夹。文档保存的名字应该是产品名.md。否则无法编译成功。

步骤三：文件夹里还有一个readme.md的文档。将这个文档打开，里面是空的。只有一个文档标题。需要在里面填入一些内容。内容可以参考[这里](https://github.com/SeeedDocument/Capacitance_Meter_Kit/blob/master/README.md). 只要改动一下SKU号还有创建日期就可以了。

你们这次修改的三个产品可能readme.md文档还是空的，如果是空的话，可以尝试着修改一下。

把readme.md文档也修改好之后。就可以将这个文件夹里的内容Git Push到Github了。和之前说的一样，用下面下个命令。
```
git add .
```
```
git commit -m"update"
```
```
git push origin master
```

## 如何将文档上传到网站
>这个步骤这次也可以忽略

上面的步骤都完成以后，就可以把新写的文档上传到我们的文档系统了。主要步骤是：
1. 将markdown文件拷贝到之前下载的Seeed-WiKi里的Docs文件夹里。
2. 回到Seeed-WiKi文件夹。右击鼠标选择"git bash", 执行以下命令。
```
bash build.sh
```
编译完后，在“site”文件夹里确认一下是否已经生成了该文档的site文件夹，里面有一个html文件。

3. 将这个site文件上传到AWS S3。
