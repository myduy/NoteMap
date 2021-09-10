### [dosbox官网](www.dosbox.com)

D盘中建立一个ASM将压缩包放进去解压

dosbox配置文件位置

打开dosbox执行

```shell
mount c: d:/ASM
c:
debug
```

可以在C:/user/$username/AppData/Local/DosBox//dosbox-xx.conf最后写入以上内容



### 安装[vim官网](www.vim.org)

在vim安装位置下配置_vimrc

前两端添加

```shell
set number
color evening
```

### demo

在dosbox下新建后缀名为asm的文件复制一下内容

```shell
assume cs:code

code segment

	
	mov box,0B008H
	mov es,bx
	
	mov bx,160*10 + 40*2
	
	mov word ptr es:[bx],5535H
	
	
	mov ax,4C00H
	int 21H
	
	
	
code ends

end
```

打开dosbox，执行

```shell
masm 文件名
link 文件名
文件名
```

也可以将以上内容添加到dosbox文件中

执行完成dosbox控制台有个紫色的的小点



### winxp使用

在masm以及link放置C:/ASM中

建立文件，内容同上

path配置环境目标位置

```shell
C:
cd ASM
masm 回车
文件名绝对路径[回车多次]
link 回车
文件名绝对路径 [回车多次]
文件名
```

执行脚本bat

```
C:
cd ASM
masm 回车
文件名绝对路径[回车多次]
link 回车
文件名绝对路径 [回车多次]
文件名
pause
```

