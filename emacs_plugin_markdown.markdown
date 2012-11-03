emacs下安装使用markdown
==========


### 下载markdown.el插件 ###

`wget http://jblevins.org/projects/markdown-mode/markdown-mode.el`

### 下载markdown解释器 ###

`download Markdown_1.0.1.zip`

**虽然是perl语言写的，不过解压之后，将其更名为markdown，然后再复制到/usr/bin/目录下即可使用。**

### 配置.emacs加载markdown.el插件 ###

**其实在markdown.el插件头几行注释写的很详细，加载即可。**

将如下代码加载到 '`.emacs`'中:

	(autoload 'markdown-mode "markdown-mode.el"
        "Major mode for editing Markdown files" t)
     (setq auto-mode-alist
        (cons '("\\.markdown" . markdown-mode) auto-mode-alist))
