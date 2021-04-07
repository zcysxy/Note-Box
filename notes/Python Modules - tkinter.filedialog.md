# Python Modules - tkinter.filedialog

[[Python Modules]]

!! filedialog 是 tkinter 模块的子模块

## 基本函数

* `.asksaveasfilename()` 生成一个选择保存路径的对话框, 返回用户选择的路径(包括文件名)
    * 如果用户取消对话框, 则返回 *None*
    * 此函数会自行建立一个选择路径下的**空文件**
* `.askopenfilename()` 生成一个选择打开路径的对话框, 返回用户选择的路径
    * 如果用户取消对话框, 则返回 *None*

## Examples

### 拷贝文本文件

```py
import tkinter.filedialog

srcFileName = tkinter.filedialog.askopenfilename()
if not srcFileName:
    exit()

dstFileName = tkinter.filedialog.asksaveasfilename()
if not dstFileName:
    exit()

f = open(srcFileName,'r')
content = f.read()
f.close

f = open(dstFileName,'w')
f.write(content)
f.close
```

其中 `exit()` 为结束程序命令

[//begin]: # "Autogenerated link references for markdown compatibility"
[Python Modules]: Python Modules "Python Modules"
[//end]: # "Autogenerated link references"