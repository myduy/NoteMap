windows启动mysql服务
$net start mysql

windows停止mysql服务
$net stop mysql

登录mysql的root账户
$mysql -u root -p

登录host主机ip为127.0.0.1=localhost的student账户
$mysql -h localhost -u student -p



| 指令	| 英文描述	| 中文描述	|
| ---- | ---- | ---- |
| ?	| 	(\?) Synonym for \`help\'	| (\?)“帮助”一样	|
| clear	| (\c) Clear the current input statement.| (\c)清除当前输入语句。	|
| connect	| (\r) Reconnect to the server. Optional arguments are db and host.	| (\r)重新连接服务器。可选参数有数据库和主机。	|
| delimiter	| (\d) Set statement delimiter.	| (\d)设置语句分隔符。|
| ego	| (\G) Send command to mysql server, display result vertically.	| (\G)发送命令到mysql服务器，垂直显示结果。	|
| exit	| (\q) Exit mysql. Same as quit.	| (\q)退出mysql。|
| go	| (\g) Send command to mysql server.	| (\g)发送命令到mysql服务器。	|
| help	| (\h) Display this help.	| (\h)显示帮助。	|
| notee	| (\t) Don't write into outfile.	| (\t)不写输出文件。	|
| print	| (\p) Print current command.	| (\p)打印当前命令。	|
| prompt	| (\R) Change your mysql prompt.	| (\R)更改mysql提示符                                          |
| quit	| (\q) Quit mysql	| (\q)退出mysql	|
| rehash 	| (\#) Rebuild completion hash.	| (\#)重建完成散列。	|
| source	| (\.) Execute an SQL script file. Takes a file name as an argument.	| (\.)执行SQL脚本文件。以文件名作为参数。	|
| status	| (\s) Get status information from the server.	| (\s)从服务器获取状态信息。	|
| system	| (\!) Execute a system shell command.	| (\ !)执行系统shell命令。 |
| tee	| (\T) Set outfile [to_outfile]. Append everything into given outfile.	| (\T)设置输出文件（输出文件）。将所有信息添加到给定的输出文件中。	|
| use	| (\u) Use another database. Takes database name as argument.	| (\u)使用其他数据库。以数据库名称作为参数。	|
| charset	| (\C) Switch to another charset. Might be needed for processing binlog with multi-byte charsets.	| (\C)切换到另一个字符集。可能需要处理带有多字节字符集的binlog。	|
| warnings	| (\W) Show warnings after every statement.	| (\W)在每个语句后显示警告。	|
| nowarning	| (\w) Don't show warnings after every statement.	| (\w)每个语句之后不显示警告；	|
| resetconnection 	| (\x) Clean session context.	| (\x)清理会话上下文。 |

\#修改字符集set character_set_client =gbk