## Jump to Section

* [Editing](#editing)
* [Search/Replace](#searchreplace)
* [Usage Search](#usage-search)
* [Compile and Run](#compile-and-run)
* [Debugging](#debugging)
* [Navigation](#navigation)
* [Refactoring](#refactoring)
* [Live Templates](#live-templates)
* [General](#general)
* [Reference](#reference)

## Editing

[[Back To Top]](#jump-to-section)

- `Ctrl + Space` **替换为：**`Ctrl + ;`
  - Basic code completion (the name of any class, method or variable)
  - 自动补全代码，可用于类、方法、变量
- `Ctrl + Shift + Space` **替换为：**`Ctrl + Shift + ;`
  - Smart code completion (filters the list of methods and variables by expected type)
  - 自动补全代码，或者列举出相应方法和变量集合
- `Ctrl + Shift + Enter`
  - Complete statement
  - 补全当前行，如：在行末尾加;完成代码；if/else代码中加上{}完成代码块
- `Ctrl + P`
  - Parameter info (within method call arguments)
  - 显示方法的参数
- `Ctrl + Q` **替换为：**`Alt + Q`
  - Quick documentation lookup
  - 显示注释文档
- `Shift + F1`
  - External Doc
  - 在浏览器中打开光标所在的类或者方法文档
- `Ctrl + mouse over code`
  - Brief Info
  - 显示类、方法、变量概要信息
- `Ctrl + F1`
  - Show descriptions of error or warning at caret
  - 显示错误或者警告信息
- `Alt + Insert`
  - Generate code... (Getters, Setters, Constructors, hashCode/equals, toString)
  - 生成代码，如：getter/setter/构造方法/...
- `Ctrl + O`
  - Override methods
  - 弹出窗口选择要Override/Implement的方法
- `Ctrl + I`
  - Implement methods
  - 弹出窗口选择要Implement的方法
- `Ctrl + Alt + T`
  - Surround with… (if..else, try..catch, for, synchronized, etc.)
  - 选择代码块，添加到if/try/for/...代码块中去
- `Ctrl + /`
  - Comment/uncomment with line comment
  - 注释/取消注释代码行：//...
- `Ctrl + Shift + /`
  - Comment/uncomment with block comment
  - 注释/取消注释代码块：/*...*/
- `Ctrl + W`
  - Select successively increasing code blocks
  - 选择连续增加的代码块（连续操作）
- `Ctrl + Shift + W`
  - Decrease current selection to previous state
  - Ctrl + W的相反操作，减少选择的代码块（连续操作）
- `Alt + Q` **替换为：**`Ctrl + Alt + Q`
  - Context info
  - 显示上下文信息，如方法/类声明，光标和声明处必须不在同一屏幕处，否则不会提示
- `Alt + Enter`
  - Show intention actions and quick-fixes
  - 显示意图采取行动和快速修复错误，可以自动导入包
- `Ctrl + Alt + L`
  - Reformat code
  - 格式化代码
- `Ctrl + Alt + O`
  - Optimize imports
  - 优化导入的类和包
- `Ctrl + Alt + I`
  - Auto-indent line(s)
  - 自动缩进行
- `Tab / Shift + Tab`
  - Indent/unindent selected lines
  - 缩进/取消缩进行
- `Ctrl + X or Shift + Delete`
  - Cut current line or selected block to clipboard
  - 删除当前行或者选择的代码块，并复制到剪切板
- `Ctrl + C or Ctrl + Insert`
  - Copy current line or selected block to clipboard
  - 复制当前行或者选择的代码块，并复制到剪切板
- `Ctrl + V or Shift + Insert`
  - Paste from clipboard
  - 从剪切板粘帖
- `Ctrl + Shift + V`
  - Paste from recent buffers...
  - 弹出窗口列举出最近使用的剪贴板内容，选择性插入
- `Ctrl + D` **替换为：**`Alt + D`
  - Duplicate current line or selected block
  - 复制当前行到下一行（未选择行时）；复制选择的代码块到选择的末尾位置
- `Ctrl + Alt + Up/Down`
  - Copy/Duplicate lines Ex
  - 复制当前行或者选择的行到上一行或者下一行（使用`Eclipse Actions`插件实现`Eclipse`同样的复制效果）
- `Ctrl + Y` **添加：**`Ctrl + D`
  - Delete line at caret
  - 删除当前行或者选择的行
- `Ctrl + Shift + J`
  - Smart line join
  - 合并选择的行为一行
- `Ctrl + Enter`
  - Smart line split
  - 拆分行
- `Shift + Enter`
  - Start new line
  - 向下插入新行
- `Ctrl + Shift + U`
  - Toggle case for word at caret or selected block
  - 大小写转换
- `Ctrl + Shift + ] / [`
  - Select till code block end/start
  - 从光标处选择代码块到结束处/开始处
- `Ctrl + Delete`
  - Delete to word end
  - 从光标处删除到单词末尾
- `Ctrl + Backspace`
  - Delete to word start
  - 从光标处删除到单词的开始
- `Ctrl + NumPad+/-`
  - Expand/collapse code block
  - 展开/折叠代码块
- `Ctrl + Shift + NumPad+`
  - Expand all
  - 展开所有的代码
- `Ctrl + Shift + NumPad-`
  - Collapse all
  - 折叠所有的代码
- `Ctrl + F4`
  - Close active editor tab
  - 关闭活动的编辑器选项卡

## Search/Replace

[[Back To Top]](#jump-to-section)

- `Double Shift`
  - Search everywhere
  - 查找源代码中的任何条目，类似于Ctrl + Shift + N
- `Ctrl + F` **只保留：**`Ctrl + F`
  - Find
  - 查找文本，支持多行查找/只在代码中查找/只在注释中查找/正则表达式
- `F3` **只保留：**`Ctrl + L`
  - Find next
  - 查找下一个，`Ctrl + F/R`之后使用
- `Shift + F3` **只保留：**`Ctrl + Shift + L`
  - Find previous
  - 查找上一个，`Ctrl + F/R`之后使用
- `Ctrl + R`
  - Replace
  - 查找替换文本，支持多行查找/只在代码中查找/只在注释中查找/正则表达式
- `Ctrl + Shift + F`
  - Find in path
  - 在指定路径/整个项目中查找文本，支持文件过滤
- `Ctrl + Shift + R`
  - Replace in path
  - 在指定路径/整个项目中查找替换文本，支持文件过滤
- `Ctrl + Shift + S`
  - Search structurally (Ultimate Edition only)
  - 搜索结构，使用模板方式查找
- `Ctrl + Shift + M`
  - Replace structurally (Ultimate Edition only)
  - 搜索替换结构，使用模板方式查找替换

## Usage Search

[[Back To Top]](#jump-to-section)

- `Alt + F7 / Ctrl + F7`
  - Find usages / Find usages in file
  - 查找类/方法/变量使用情况。`Ctrl + F7`只找当前文件
- `Ctrl + Shift + F7`
  - Highlight usages in file
  - 查找类/方法/变量使用情况，只找当前文件。类似于`Ctrl + F`效果
- `Ctrl + Alt + F7`
  - Show usages
  - 弹出列表窗口，显示出指定的类/方法被使用情况

## Compile and Run

[[Back To Top]](#jump-to-section)

- `Ctrl + F9`
  - Make project (compile modifed and dependent)
  - 编译项目
- `Ctrl + Shift + F9`
  - Compile selected file, package or module
  - 编译选中的文件/包/模块
- `Alt + Shift + F10`
  - Select configuration and run
  - 选择指定配置/文件运行
- `Alt + Shift + F9`
  - Select configuration and debug
  - 选择指定配置/文件调试
- `Shift + F10` **替换为：**`Shift + F9`
  - Run
  - 运行
- `Shift + F9` **替换为：**`F9`
  - Debug
  - 调试
- `Ctrl + Shift + F10`
  - Run context configuration from editor
  - 从编辑器中的上下文配置运行，如：jUnit的test方法，ant中...

## Debugging

[[Back To Top]](#jump-to-section)

- `F8` **替换为：**`F6`
  - Step over
  - 逐行执行
- `F7` **替换为：**`F5`
  - Step into
  - 进入方法内部
- `Alt + Shift + F7`
  - Force step into
  - 强制进入方法内部
- `Shift + F7`
  - Smart step into
  - 智能进入方法内部
- `Shift + F8` **替换为：**`F7`
  - Step out
  - 跳出方法
- `Alt + F9`
  - Run to cursor
  - 运行到光标处所在的行
- `Alt + F8`
  - Evaluate expression
  - 弹出窗口，输入验证表达式
- `F9` **替换为：**`F8`
  - Resume program
  - 跳到下一个断点，或者恢复运行（最后一个断点情况下）
- `Ctrl + F8`
  - Toggle breakpoint
  - 当前行添加/删除断点
- `Ctrl + Shift + F8`
  - View breakpoints
  - 查看所有断点信息
- `Ctrl + Alt + R`
  - Reload Changed Classes
  - 重新加载更改过代码的class（用于调试时，更改代码后不重启环境生效，不一定会起作用，如：涉及静态的）

## Navigation

[[Back To Top]](#jump-to-section)

- `Ctrl + N`
  - Go to class
  - 查找类
- `Ctrl + Shift + N`
  - Go to file
  - 查找文件
- `Ctrl + Alt + Shift + N`
  - Go to symbol
  - 查找方法
- `Alt + Right/Left` **替换为：**`Ctrl + Alt + Left/Right`
  - Go to next/previous editor tab
  - 切换到右边/左边的编辑窗口
- `F12`
  - Go back to previous tool window
  - 切换到最近使用的工具栏窗口
- `Esc`
  - Go to editor (from tool window)
  - 在工具栏窗口切换到编辑窗口
- `Shift + Esc`
  - Hide active or last active window
  - 隐藏当前（或最后活动的）工具窗口，并切换到编辑窗口
- `Ctrl + Shift + F4`
  - Close active run/messages/find/... tab
  - 关闭活动选项卡
- `Ctrl + G`
  - Go to line
  - 定位到指定行号
- `Ctrl + E`
  - Recent files popup
  - 弹出窗口列举出最近访问的文件
- `Ctrl + Alt + Left/Right` **替换为：**`Alt + Right/Left`
  - Navigate back/forward
  - 导航向前/后退
- `Ctrl + Shift + Backspace` **替换为：**`Ctrl + Q`
  - Navigate to last edit location
  - 导航到最近编辑的位置（可以连续操作）
- `Alt + F1`
  - Select current file or symbol in any view
  - 定位文件/方法的位置在指定的视图下，如：项目结构/包目录/方法集合/磁盘位置等
- `Ctrl + B or Ctrl + Click`
  - Go to declaration
  - 跳转到类/方法/变量定义处
- `Ctrl + Alt + B` **添加：**`Ctrl + T`
  - Go to implementation(s)
  - 跳转到实现
- `Ctrl + Shift + I`
  - Open quick definition lookup
  - 显示光标处类/方法/变量的定义信息
- `Ctrl + Shift + B` **增加：**`F3`
  - Go to type declaration
  - 跳转到类型的定义处
- `Ctrl + U`
  - Go to super-method/super-class
  - 跳转到父方法/父类
- `Alt + Up/Down`
  - Go to previous/next method
  - 跳转上一个/下一个方法
- `Ctrl + ] / [`
  - Move to code block end/start
  - 移动到代码块结束处/开始处，并高亮{}
- `Ctrl + F12`
  - File structure popup
  - 显示当前文件的结构，可以进行方法快速过滤定位
- `Ctrl + H`
  - Type hierarchy
  - 显示类结构图（类的继承层次）
- `Ctrl + Shift + H`
  - Method hierarchy
  - 显示方法结构图（方法的继承层次）
- `Ctrl + Alt + H`
  - Call hierarchy
  - 显示方法被调用结构图
- `F2 / Shift + F2`
  - Next/previous highlighted error
  - 定位到上一个/下一个错误或警告，并高亮
- `F4 / Ctrl + Enter`
  - Edit source / View source
  - 在视图窗口中选择文件/方法等，快速跳转到编辑窗口中
- `Alt + Home`
  - Show navigation bar
  - 光标定位到导航拦
- `F11`
  - Toggle bookmark
  - 添加/删除标签（当前行）
- `Ctrl + F11`
  - Toggle bookmark with mnemonic
  - 以指定数字或者字母做为添加书签；删除书签
- `Ctrl + #[0-9]`
  - Go to numbered bookmark
  - 跳转到指定标记的书签，配合`Ctrl + F11`使用
- `Shift + F11`
  - Show bookmarks
  - 显示所有的标签

## Refactoring

[[Back To Top]](#jump-to-section)

- `F5` **替换为：**`Shift + F10`
  - Copy
  - 复制当前类或者文件
- `F6` **替换为：**`F10`
  - Move
  - 移动类/方法/文件
- `Alt + Delete`
  - Safe Delete
  - 安全方式删除
- `Shift + F6` **替换为：**`Ctrl + Shift + R`
  - Rename
  - 重命名方法/类/文件
- `Ctrl + F6` `快捷键已取消`
  - Change Signature
  - 更改签名
- `Ctrl + Alt + N`
  - Inline
  - 将方法/类重构为内联方法/匿名类
- `Ctrl + Alt + M`
  - Extract Method
  - 提取选中的代码块生成一个新的方法
- `Ctrl + Alt + V`
  - Extract Variable
  - 提取选中的代码块生成一个新的变量
- `Ctrl + Alt + F`
  - Extract Field
  - 提取选中的代码块生成一个新的属性
- `Ctrl + Alt + C`
  - Extract Constant
  - 提取选中的代码块生成一个新的常量
- `Ctrl + Alt + P`
  - Extract Parameter
  - 提取选中的代码块生成一个新的参数

## Live Templates

[[Back To Top]](#jump-to-section)

- `Ctrl + Alt + J`
  - Surround with Live Template
  - 选择代码块，添加到模板代码块中去
- `Ctrl + J`
  - Insert Live Template
  - 插入模板代码
    - iter Iteration according to Java SDK 1.5 style
    - inst Check object type with instanceof and downcast it
    - itco Iterate elements of java.util.Collection
    - itit Iterate elements of java.util.Iterator
    - itli Iterate elements of java.util.List
    - psf public static final
    - thr throw new

## General

[[Back To Top]](#jump-to-section)

- `Alt + #[0-9]`
  - Open corresponding tool window
  - 打开相应的工具窗口
- `Ctrl + S`
  - Save all
  - 保存所有的文件
- `Ctrl + Alt + Y`
  - Synchronize
  - 同步文件到磁盘
- `Ctrl + Shift + F12`
  - Toggle maximizing editor
  - 切换最大化编辑器
- `Alt + Shift + F`
  - Add to Favorites
  - 添加到收藏夹
- `Alt + Shift + I`
  - Inspect current file with current profile
  - 检查当前文件与当前的配置文件
- ``Ctrl + BackQuote (`)``
  - Quick switch current scheme
  - 快速切换配置信息，如：皮肤/快捷键/格式化代码风格等
- `Ctrl + Alt + S`
  - Open Settings dialog
  - 打开设置对话框
- `Ctrl + Alt + Shift + S`
  - Open Project Structure dialog
  - 打开项目结构设置对话框
- `Ctrl + Shift + A`
  - Find Action
  - 查找菜单功能/快捷键设置/配置等信息
- `Ctrl + Tab`
  - Switch between tabs and tool window
  - 标签和工具窗口之间切换，选择完成之前需要先按住`Ctrl`键不放，`Up/Down/[0-9]/[a-z]`选择相应的编号

## Reference

[[Back To Top]](#jump-to-section)

> Win Keymap [Win Keymap](http://www.jetbrains.com/idea/docs/IntelliJIDEA_ReferenceCard.pdf)

> Mac OS Keymap [Mac OS Keymap](http://www.jetbrains.com/idea/docs/IntelliJIDEA_ReferenceCard_Mac.pdf)
