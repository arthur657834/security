```
npm install -g hexo


mkdir blog
cd blog
npm install hexo-deployer-git --save （这命令是为了解决hexo新版本的部署问题）
hexo init
npm install
hexo g
#生成静态页面
hexo s

目录解析：
node_modules：是依赖包
public：存放的是生成的页面
scaffolds：命令生成文章等的模板
source：用命令创建的各种文章
themes：主题
_config.yml：整个博客的配置
db.json：source解析所得到的
package.json：项目所需模块项目的配置信息


github新建参考arthur.github.io

vi _config.yml
deploy:
  type: git
  repo: https://github.com/arthur657834/arthur.github.io.git
  branch: master

配置文件解析：
1. 修改网站相关信息

title: inerdstack
subtitle: the stack of it nerds
description: start from zero
author: inerdstack
language: zh-CN
timezone: Asia/Shanghai

language和timezone都是有输入规范的，详细可参考语言规范和时区规范。
https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes
https://en.wikipedia.org/wiki/List_of_tz_database_time_zones

注意：每一项的填写，其:后面都要保留一个空格，下同。

2. 配置统一资源定位符（个人域名）

url: http://inerdstack.com
对于root（根目录）、permalink（永久链接）、permalink_defaults（默认永久链接）等其他信息保持默认。

新建blog：
1.
  hexo new "文章标题"
  source->_post文件夹下看到我们新建的markdown文件
  hexo server

2.
  可以手动添加Markdown文件在source->_deploy文件夹下

发布到github
hexo clean
hexo generate
hexo deploy

更换主题：
https://github.com/hexojs/hexo/wiki/Themes
cd themes
git clone git://github.com/ppoffice/hexo-theme-alex.git

```
