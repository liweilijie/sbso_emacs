## install cscope ##
source code install cscope

* * * * *

## then config .emacs ##
	;; This is liwei's emacs config file
;;
;;
;; Set Default Load path
(add-to-list 'load-path "~/.liw_emacs.d")

(autoload 'markdown-mode "markdown-mode.el"
        "Major mode for editing Markdown files" t)
     (setq auto-mode-alist
        (cons '("\\.markdown" . markdown-mode) auto-mode-alist))
(custom-set-variables
  ;; custom-set-variables was added by Custom.
  ;; If you edit it by hand, you could mess it up, so be careful.
  ;; Your init file should contain only one such instance.
  ;; If there is more than one, they won't work right.
 '(inhibit-startup-screen t))
(custom-set-faces
  ;; custom-set-faces was added by Custom.
  ;; If you edit it by hand, you could mess it up, so be careful.
  ;; Your init file should contain only one such instance.
  ;; If there is more than one, they won't work right.
 )

## 找到xcscope.el文件，将其放在~/.liw_emacs.d目录下 ##

## 然后在.emacs里面增加加载命令(require 'xcscope) ##

## cscope-indexer -r ##

## 快捷键命令 ##
> C-c s s : Find symbol.
> C-c s d : Find global definition.
> C-c s g : Find global definition(alternate binding).
> C-c s G : Find global definitoin without prompting.
> C-c s c : Find functions calling a function.
> C-c s C : Find called functions(list functions called from a function)
> C-c s t : Find text string.
> C-c s e : find egrep pattern.
> C-c s f : find a file.
> C-c s i : Find files #include a file
