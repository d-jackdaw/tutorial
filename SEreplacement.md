## 教程：游戏内音效替换
假设你想把游戏司辰之书（book of hours）内的音效替换成otto鬼叫，该怎么做？

## 前提
游戏为unity制作。可以通过查看游戏文件（比如`C:\Program Files (x86)\Steam\steamapps\common\Book of Hours\bh_Data`）来判断。

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

### 准备音频
1. 准备otto鬼叫音频。
2. 打开游戏文件目录，比如 `C:\Program Files (x86)\Steam\steamapps\common\Book of Hours\bh_Data`。这时，你可以看到一堆.assets文件。
3. 打开 AS，选择上边栏的 File ，选择 Load File，打开游戏文件目录里的 `globalgamemanagers`（没有后缀名的那个）。
4. 点击上边栏下方的 Asset List，可以看到包内文件列表。
5. 游戏音频文件的格式为 `AudioClip`。点击上边栏的 Filter Type，可以选择只查看 `AudioClip`。这时，你就可以随意选择音频文件播放了。
6. 记下你想替换哪些游戏音效。对文件名右键，选择 Copy text 来拷贝文件名称。这里我推荐新建一个笔记本，来逐行写下 想替换的音频文件名 和 想替换成什么otto鬼叫的名称。
7. 将otto鬼叫音频重命名为你想替换的音频文件名。比如，将 哇袄.wav 重命名成 book.drop.1.wav，这意味着将放下书籍的音效替换成哇袄。
![SEreplacement_1](https://github.com/user-attachments/assets/cb02fb48-c4cd-464f-a396-b87929c10d2f)

### 生成unity文件
8. 打开unity。选择 New Project 创建新文件，选择 2D (Built-in 后面省略)，输入你的 Project name（项目名称） ，选择 Location（存放项目的文件夹），Create Project。多等一会儿，unity很慢的啦。
9. 进入unity界面。左边栏是场景内文件，这里我习惯将 Main Camera 等场景文件删除。
10. 把刚才重命名后的otto鬼叫音频拖到界面下方的位置，然后再从下方拖到左边栏。这时你可以看到场景内多了喇叭图标。

![SEreplacement_2](https://github.com/user-attachments/assets/b09becfb-f044-448a-bbdd-84a6a326e7b9)

11. 点击上边栏的 File，选择 Build Settings，在弹出的页面中选择 Build。这时可能会提示需要新建文件夹来储存，照着做就行。在接下来的弹窗中选择 save。这样你就生成了一个unity文件。

![SEreplacement_3](https://github.com/user-attachments/assets/c233daa4-79a1-4cbd-acb0-db79b7fed3d7)

12. 打开unity文件所在的文件夹，打开 项目名称_Data 文件夹。将 `sharedassets0.resource` 重命名。这里，我将其更改成 `otto.resource`。
    
![SEreplacement_4](https://github.com/user-attachments/assets/00a63398-aa3a-4d1b-a5db-f12b843be6d9)

### 修改dunp
13. 打开UABEA。选择上边栏的 File ，选择 Open，打开游戏文件目录里的 `globalgamemanagers`（没有后缀名的那个）。UABEA可以通过点击上边栏的 View 后选择 Filter 来只查看 `AudioClip`。
14. 找到自己想修改的游戏音效文件。点击右侧的 `Export Dump`，新建一个文件夹保存。这里，我新建了一个名为 dumps 的文件夹。在弹出的 Select dump type 窗口中，选择默认的 `UABE text dump`。

![SEreplacement_5](https://github.com/user-attachments/assets/4ae7b571-5a96-40af-8a43-e237e8b76b1c)

15. 打开导出dumps文件的文件夹。文件名大致如图所示。对于这些txt dump文件，需要逐个进行2个改动： 
   - 文件名重命名为游戏音效文件的原名。比如，将 `Bees-sharedassets0.assets-337.txt` 改为 `Bees.txt`
   - 打开txt文件，将 `1 string m_Source = "sharedassets0.resource"` 改为 `1 string m_Source = "otto.resource`（即【第12步】重命名后的名称）
   - 对每个txt都要进行上述改动！

![SEreplacement_6](https://github.com/user-attachments/assets/d670d9ff-8ca6-4e79-8350-7323a5ddc35c)

### 修改游戏文件
16. 打开UABEA。再次打开游戏文件目录里的 `globalgamemanagers`。找到自己想修改的游戏音效文件。点击右侧的 `Import Dump`，选择刚才修改的、名称与之对应的txt dump文件，选择打开。这样，就将修改后的dump文件导入到游戏文件当中了。
17. ***先别急着保存！*** 全部 `import dump` 后，点击上边栏的 File，选择 Save as，在下方的文件名这一栏，改成类似 ***sharedassets0!.assets*** 的名称。***千万不能和原文件一样！*** 有时可能会导出其他名称的.assets文件，这是因为游戏音频可能保存在其他的.assets里面，同样的道理，改成和原文件不同的名称保存。
18. 打开游戏文件目录。新建backup文件夹，将原来的 `sharedassets0.assets` 拖进去。
19. 找到我们新建的 `otto.resource` 和 `sharedassets0!.assets`，放在游戏文件目录内。将 `sharedassets0!.assets` 重命名为 `sharedassets0.assets`。

### 验证
20. 打开UABEA。再次打开游戏文件目录里的 `globalgamemanagers`。找到自己修改过的游戏音效文件。点击右侧的 `Plugins`，在弹出的窗口点击 `Export audio file`。如果能成功导出，就是成功了！
21. 开始游戏~
