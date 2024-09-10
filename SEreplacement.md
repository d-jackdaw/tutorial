## 教程：游戏内音效替换
假设你想把游戏司辰之书（book of hours）内的音效替换成otto鬼叫，该怎么做？

## 前提
游戏为unity制作。这个可以通过查看游戏文件（比如`C:\Program Files (x86)\Steam\steamapps\common\Book of Hours\bh_Data`）来判断。

## 软件准备
### 必备
- unity：用于给音效包制作.resource和.asset。
- UABEA：用于导入dump和保存修改后的.asset。和UABE完全一致，适配2022年后unity。
- AssetStudio：下文简称“AS”。用于快速查看.asset内文件，比如音频。对于2022年后的unity可能会频繁报错。
### 可选
- AssetRipper：如果受不了AS报错可以用这个代替。无GUI，操作界面在浏览器上，比较麻烦。
### 锦上添花
- Audacity：音频编辑软件。可以剪辑音频，给音频加效果器（比如混响）。

## 流程
1. 准备otto鬼叫音频。
2. 打开游戏文件目录，比如 `C:\Program Files (x86)\Steam\steamapps\common\Book of Hours\bh_Data`。这时，你可以看到一堆.assets文件。
3. 用AS打开 `globalgamemanagers`（没有后缀名的那个），点击搜索栏上方的 Asset List，可以看到包内文件列表。
4. 游戏音频文件的格式为 `AudioClip`。点击上边栏的 Filter Type，可以选择只查看 `AudioClip`。这时，你就可以随意选择音频文件播放了。
5. 记下你想替换哪些游戏音效。
   对文件名右键，可以 Copy text (拷贝文件名称)。
   这里我推荐新建一个笔记本，来逐行写下 想替换的音频文件名 和 想替换成什么otto鬼叫的名称。

![SEreplacement_1](https://github.com/user-attachments/assets/cb02fb48-c4cd-464f-a396-b87929c10d2f)

6. 将otto鬼叫音频重命名为你想替换的音频文件名。比如，将 哇袄.wav 重命名成 book.drop.1.wav，这意味着将放下书籍的音效替换成哇袄。
7. 打开unity。选择 New Project 创建新文件，选择 2D (Built-in 后面省略)，输入你的 Project name（项目名称） ，选择 Location（存放项目的文件夹）， Create Project。多等一会儿，unity很慢的啦。
8. 
