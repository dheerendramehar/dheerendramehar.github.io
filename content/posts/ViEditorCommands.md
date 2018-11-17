+++
title = "vi editor useful commands"
date = 2018-10-23T00:01:34+05:30
tags = [""]
categories = [""]
draft = false
+++

| 			Description   			| 	Command 	|
| 			-----------				|   ------- 	|
| comment all the lines 			| <font face="Consolas" size="4"> :%s/^/# </font>  |
| uncommnet all the lines 			| <font face="Consolas" size="4"> :%s/^#/ </font>  |
| comment line no. m to n			| <font face="Consolas" size="4"> :m,ns/^/# </font>  |
| uncomment line no. m to n 		| <font face="Consolas" size="4"> :m,ns/^#/ </font>  |
| add comma after all the lines 	| <font face="Consolas" size="4"> :%s/$/, </font>  |
| remove comma after all the lines 	| <font face="Consolas" size="4"> :%s/,$/ </font>  |
| remove comma after line no. m to n |<font face="Consolas" size="4"> :m,ns/,$/ </font>  |
| search for a string from forward	| <font face="Consolas" size="4"> /string </font>  |
| search for a string from backward	| <font face="Consolas" size="4"> ?string </font>  |
| repeat the search in same direction |<font face="Consolas" size="4"> n </font>  |
| repeat the search in reverse direction  | <font face="Consolas" size="4"> N </font>  |
| delete a line 					| <font face="Consolas" size="4"> dd </font>  |
| delete n lines 					| <font face="Consolas" size="4"> ndd </font>  |
| delete nth line					 | <font face="Consolas" size="4"> :nd </font>  |
| delete line no. m to n			| <font face="Consolas" size="4"> :m,nd </font>  |
| copy a line  						| <font face="Consolas" size="4">  yy </font>  |
| copy n lines  					| <font face="Consolas" size="4"> nyy </font>  |
| copy nth line 					| <font face="Consolas" size="4"> :ny </font>  |
| copy line no. m to n				| <font face="Consolas" size="4"> :m,ny </font>  |
| put or paste a line 				 | <font face="Consolas" size="4"> p </font>  |
| running a command without exiting vi | <font face="Consolas" size="4"> :!<command> </font>  |
| undo last change					| <font face=" Consolas"> u </font>  |
| redo last change					| <font face="Consolas" size="4"> Ctrl + r </font>  |
| write to a file                	| <font face="Consolas" size="4">  :w <file_name> </font>  |
| write and quit					| <font face="Consolas" size="4"> :wq </font>  |
| quit forcefully without saving changes | <font face="Consolas" size="4"> q! </font>  |
| move cursor to start of current line | <font face="Consolas" size="4"> ^ </font>  |
| move the cursor to end of current line | <font face="Consolas" size="4"> $ </font>  |
| move cursor to start of current line | <font face="Consolas" size="4"> 1G </font>  |
| move the cursor to end of current line | <font face="Consolas" size="4"> G </font>  |
| move the cursor to nth line | <font face="Consolas" size="4"> nG </font>  |
| delete a line after the cursor  | <font face="Consolas" size="4"> C </font> |

Please let me know, if there is any error in above commands.




