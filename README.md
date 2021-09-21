预览地址：[https://iengu.github.io](https://iengu.github.io)   

### 主题介绍
一个基于hexo系统个人博客主题，全站自适应双栏布局，深色色块板块区分，风格简单干净，整体现代感较强，适合科技、技术、文字类博客使用。本主题内ICON图标使用第三方图标库 [font-awesome](https://fontawesome.com/)。

### 使用指南
* 克隆项目到HEXO博客根目录themes文件夹下
```
git clone --depth=1 https://github.com/iengu/hexo-theme-mokusei.git themes/mokusei
```
* 更改博客配置文件_config.yml, theme选项值设为mokusei
```
_config.yml

- theme: other themes
+ theme: mokusei
```
* 关于代码高亮  (更改博客配置文件_config.yml为以下推荐配置)
```
_config.yml

highlight:
  enable: true
  line_number: false
  auto_detect: false
  tab_replace: ''
  wrap: false
  hljs: true
prismjs:
  enable: false
  preprocess: true
  line_number: true
  tab_replace: ''
```
* 主题内详细配置请见：[wiki](https://github.com/iengu/hexo-theme-mokusei/wiki/%E4%B8%BB%E9%A2%98%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6_config.yml)
* 更新主题
```
cd themes/mokusei
git pull origin master
```

### 关于多语言支持

可以使用Mokusei来实现多语言站点，类似于Hexo和Vue.js的官网。

实现方式比较特殊：你需要将不同语言独立为不同的站点。每个站点都是public下的二级子目录，这样只用一个域名就可以实现多语言功能。默认语言直接使用网站根目录。

而为了确保不同语言拥有各自的文章内容，防止混杂，**它们放在各自的源文件夹中**。本方案不支持同一文章的多语言切换。

**第一步，修改站点配置文件**。你需要为每个语言使用各自的配置文件，并修改下面**单独列出**的字段，例如：

- 默认语言（中文，`_config.yml`）：
```yaml
url: https://username.github.io/
root: /           # 站点路径的根目录，可以不写此字段

public: public    # 站点输出目录
source: source    # 中文版页面专属的源文件目录
```

- 次语言（英文，`_config_en.yml`）：
```yaml
# 这里参照了Hexo官方文档的提示
url: https://username.github.io/en
root: /en/        # 站点路径的根目录，设定为站点的目录

public: public/en # 站点输出目录
source: source-en # 英文版页面专属的源文件目录
```

**第二步，配置主题的`_config.yaml`**：

```yaml
i18n:
  languageList:           # 指定可用于切换的多语言列表，值为你语言对应的网站二级目录
    zh-cn:
      name: 简体中文      # 指定语言的显示名称 
    en:
      name: English
  default: zh-cn          # 指定默认语言，即直接使用根目录访问网站时的语言
  showSwitcher: true      # 是否在导航栏中显示语言切换器
```

**第三步，分别生成不同语言的站点**。

**注意在每次生成前都要删除站点根目录下的`db.json`，否则所有语言的博文将混在一起。**

```bash
rm -f db.json
hexo g            # 生成默认语言站点

rm -f db.json
hexo g --config   # 生成英文站点
```

如果需要更改语言切换器在导航栏的位置，请自行修改导航栏的源代码（`layout/_partial/nav.ejs`）。

