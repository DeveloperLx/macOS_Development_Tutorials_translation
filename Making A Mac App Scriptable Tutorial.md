# 让Mac App可脚本化的教程

#### [原文地址](https://www.raywenderlich.com/133007/making-mac-app-scriptable-tutorial) 翻译：[DeveloperLx](http://weibo.com/DeveloperLx)

<div class="content-wrapper">
    <div class="note">
        <p>
            <em>
                16年9月21日更新：
            </em>
            这个教程已更新至Xcode 8及Swift 3。
        </p>
    </div>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/05/MacAppScriptable-feature-250x250.png"
        alt="Making a mac app scriptable tutorial: feature image" width="250" height="250"
        class="alignright size-thumbnail wp-image-135425" srcset="https://koenig-media.raywenderlich.com/uploads/2016/05/MacAppScriptable-feature-250x250.png 250w, https://koenig-media.raywenderlich.com/uploads/2016/05/MacAppScriptable-feature-320x320.png 320w, https://koenig-media.raywenderlich.com/uploads/2016/05/MacAppScriptable-feature.png 500w, https://koenig-media.raywenderlich.com/uploads/2016/05/MacAppScriptable-feature-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2016/05/MacAppScriptable-feature-64x64.png 64w, https://koenig-media.raywenderlich.com/uploads/2016/05/MacAppScriptable-feature-96x96.png 96w, https://koenig-media.raywenderlich.com/uploads/2016/05/MacAppScriptable-feature-128x128.png 128w"
        sizes="(max-width: 250px) 100vw, 250px">
    </p>
    <p>
        作为一个app开发者，几乎是不可能想到人们
        <i>
            所有的
        </i>
        使用你app的方法的。如果能让你的用户创建脚本，来定制你的app去满足他们个人化的需求，难道不是很酷？
    </p>
    <p>
        使用Applescript和Javascript来自动化（JXA），你可以！在这个让mac app可脚本化的教程中，你将了解到，怎样添加脚本的处理的能力到示例应用上。你将从了解怎样使用脚本控制存在的app开始，然后扩展一个app去允许定制脚本行为。
    </p>
    <h2>
        开始吧
    </h2>
    <p>
        下载
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/07/ScriptableTasks-Starter2.zip">
            示例工程
        </a>
        ，在Xcode中打开并运行，查看它的样子：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/Scriptable-Tasks-app.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/04/Scriptable-Tasks-app-700x389.png"
            alt="Making a mac app scriptable tutorial: Scriptable Tasks app" width="700"
            height="389" class="aligncenter size-large wp-image-133026" srcset="https://koenig-media.raywenderlich.com/uploads/2016/04/Scriptable-Tasks-app.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/04/Scriptable-Tasks-app-480x267.png 480w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        这个app展示了一个带有到期日的，在接下来几天的任务的列表，还有关联到每个任务的标签。它使用一个outline view来根据到期日给任务分租。
    </p>
    <div class="note">
        <em>
            注意：
        </em>
        想要了解更多关于outline view的事？在这个文章中查看
        <a href="https://github.com/DeveloperLx/macOS_Development_Tutorials_translation/blob/master/NSOutlineView%20on%20macOS%20Tutorial.md">
            OS X的教程NSOutlineView
        </a>
        。
    </div>
    <p>
        你可能注意到，你不能添加，编辑，或删除任务。这是由设计决定的 - 这些动作将通过你的用户的自动化脚本来处理。
    </p>
    <p>
        看一下项目中的文件：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/ScriptableTasksProject.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/04/ScriptableTasksProject-334x500.png"
            alt="Making a mac app scriptable tutorial: Scriptable Tasks Project" width="334"
            height="500" class="aligncenter size-large wp-image-133011" srcset="https://koenig-media.raywenderlich.com/uploads/2016/04/ScriptableTasksProject-334x500.png 334w, https://koenig-media.raywenderlich.com/uploads/2016/04/ScriptableTasksProject-214x320.png 214w, https://koenig-media.raywenderlich.com/uploads/2016/04/ScriptableTasksProject.png 496w"
            sizes="(max-width: 334px) 100vw, 334px">
        </a>
    </p>
    <ul>
        <li>
            有两个模型类的文件：
            <em>
                Task.swift
            </em>
            和
            <em>
                Tag.swift
            </em>
            。这是你将要编写的类。
        </li>
        <li>
            <em>
                ViewController
            </em>
            这组处理展示和观察数据的变化。
        </li>
        <li>
            <em>
                Data
            </em>
            组有一个带有示例任务的文件，还有一个
            <em>
                DataProvider
            </em>
            来读取那些任务，并处理到达的任何修改。
        </li>
        <li>
            这个
            <em>
                AppDelegate
            </em>
            使用一个
            <code>
                DataProvider
            </code>
            对象来持有一个app任务的记录。
        </li>
        <li>
            <em>
                ScriptableTasks.sdef
            </em>
            是一个重要的文件...你将要在之后详细地探索。
        </li>
    </ul>
    <p>
        本教程还有一些示例脚本；
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/07/SampleScripts2.zip">
            从这里下载
        </a>
        。在这个包中有两个目录：一个用于AppleScript，另一个用于JavaScript。由于这个教程的重点不在于写脚本，你将使用每一个下载到的脚本来测试你将添加到
        <em>
            Scriptable Tasks
        </em>
        中的功能。
    </p>
    <p>
        说得已经足够了 - 是时候移步到脚本这里了！:]
    </p>
    <h2>
        使用脚本编辑器
    </h2>
    <p>
        打开
        <em>
            Applications/Utilities
        </em>
        中的
        <em>
            Script Editor app
        </em>
        ，并打开一个新的文档：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/ScriptEditor.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/04/ScriptEditor-496x500.png"
            alt="Making a mac app scriptable tutorial: Script Editor" width="496" height="500"
            class="aligncenter size-large wp-image-133009" srcset="https://koenig-media.raywenderlich.com/uploads/2016/04/ScriptEditor-496x500.png 496w, https://koenig-media.raywenderlich.com/uploads/2016/04/ScriptEditor-318x320.png 318w, https://koenig-media.raywenderlich.com/uploads/2016/04/ScriptEditor-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2016/04/ScriptEditor-64x64.png 64w, https://koenig-media.raywenderlich.com/uploads/2016/04/ScriptEditor-96x96.png 96w, https://koenig-media.raywenderlich.com/uploads/2016/04/ScriptEditor-128x128.png 128w, https://koenig-media.raywenderlich.com/uploads/2016/04/ScriptEditor.png 700w"
            sizes="(max-width: 496px) 100vw, 496px">
        </a>
    </p>
    <p>
        你将在顶部的工具栏中看到四个按钮：
        <em>
            Record
        </em>
        ，
        <em>
            Stop
        </em>
        ，
        <em>
            Run
        </em>
        ，和
        <em>
            Compile
        </em>
        。Compile检查你的脚本是语法正确的，而Run做的大致就是你所期望的。
    </p>
    <p>
        而在window的底部，你会看到三个图标，用来在view之间切换。
        <em>
            Description
        </em>
        让你添加一些关于你的脚本的信息，而
        <em>
            Result
        </em>
        则展示了你运行一个脚本最后的结果。最有用的选项则是第三个按钮：
        <em>
            Log
        </em>
        。
    </p>
    <p>
        而Log还提供了四个选项：
        <em>
            Result
        </em>
        ，
        <em>
            Messages
        </em>
        ，
        <em>
            Events
        </em>
        和
        <em>
            Replies
        </em>
        。Replies是信息量最大的，因为它展示了每个命令和命令返回的值。当测试任何脚本的时候，我强烈推荐
        <em>
            Log in Replies
        </em>
        模式。
    </p>
    <div class="note">
        <p>
            <em>
            	注意：
                Note:
            </em>
            如果你曾经打开过一个AppleScript文件，并发现它包含类似下面的代码：
            <code>
                «class TaSk» whose «class TrFa» is false and «class CrDa»
            </code>
            ，点击
            <em>
                Compile
            </em>
            ，它将转变为可读的AppleScript，前提是你已安装了目标的app。
        </p>
    </div>
    <p>
	    在这个教程中，你将cover到两种脚本语言。第一种是AppleScript，它是在1991年的Mac系统7是被引入的，使其可以被码农和非码农使用。
    </p>
    <p>
    	第二种则是JavaScript for Automation (JXA)，它是在OSX Yosemite系统中被引用的，让码农可以使用它们熟悉的JavaScript语法来构建它们的自动化任务。
    </p>
    <p>
    	在本教程中的脚本将同时通过AppleScript和JXA来展现，因此你可以自由地沿着你想要探索那种语言去漫游。:]
    </p>
    <div class="note">
        <p>
            <em>
            	注意：
            </em>
            在本教程中，脚本的代码片段将首先通过AppleScript来展示，之后则紧跟着等效的JavaScript的版本。
        </p>
    </div>
    <h3>
        使用TextEdit探索App脚本
    </h3>
    <p>
        有一个很棒的小app早已安装到了你的Mac上：TextEdit，它支持脚本的撰写。在
        <em>
            Script Editor
        </em>
        中，选择
        <em>
            Window/Library
        </em>
        并找到
        <em>
            TextEdit
        </em>
        的入口。如果它不在这里，单击顶部的
        <em>
            Plus
        </em>
        按钮，找到你的
        <em>
            Applications
        </em>
        目录并添加
        <em>
            TextEdit
        </em>
        。然后双击
        <em>
            TextEdit
        </em>
        入口来打开TextEdit字典：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/TextEditDictionary.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/04/TextEditDictionary-593x500.png"
            alt="Making a mac app scriptable tutorial: Text Edit Dictionary" width="593"
            height="500" class="aligncenter size-large wp-image-133021" srcset="https://koenig-media.raywenderlich.com/uploads/2016/04/TextEditDictionary-593x500.png 593w, https://koenig-media.raywenderlich.com/uploads/2016/04/TextEditDictionary-380x320.png 380w, https://koenig-media.raywenderlich.com/uploads/2016/04/TextEditDictionary.png 700w"
            sizes="(max-width: 593px) 100vw, 593px">
        </a>
    </p>
    <p>
        每一个可编写脚本的app有一个字典，储存在脚本的定义文件（SDEF）中。这个字典告诉你这个app中包含哪些对象，这些对象中包含什么属性，这个app能响应什么命令。在上面的屏幕截图中，你可以看到TextEdit含有若干个段落，这些段落含有颜色和字体的特性。你将使用这些信息来风格化一些文本。
    </p>
    <p>
        从
        <em>
            AppleScript
        </em>
        或
        <em>
            JavaScript
        </em>
        目录中打开
        <em>
            1. TextEdit Write.scpt
        </em>
        目录。运行脚本；你将看到TextEdit创建并保存了一个文档。
    </p>
    <p>
        现在你有了一个新的文档，但它需要一点样式。打开
        <em>
            2. TextEdit Read Edit.scpt
        </em>
        ，运行这个脚本，你将看到这个文档根据脚本再次打开并样式化。
    </p>
    <p>
        尽管深入钻研实际的脚本超过了这个教程的范围，也请随意仔细阅读脚本，来查看它如何在TextEdit的文档上执行。
    </p>
    <p>
        正如在介绍中提到的，所有的app在一定程度上都是可脚本化的。为了看到这个起作用，确保Scriptable的任务正在执行。下一步，在Script Editor中打开一个新的脚本window并输入下列脚本中的一个，取决于你正在使用的语言：
    </p>
    <pre class="applescript" style="font-family:monospace;"><span style="color: #808080; font-style: italic;">-- AppleScript</span>
<span style="color: #ff0033; font-weight: bold;">tell</span> <span style="color: #0066ff;">application</span> <span style="color: #009900;">"Scriptable Tasks"</span> <span style="color: #ff0033; font-weight: bold;">to</span> <span style="color: #0066ff;">quit</span></pre>
    <p>
        或
    </p>
    <pre class="javascript" style="font-family:monospace;"><span style="color: #006600; font-style: italic;">// JavaScript</span>
Application<span style="color: #009900;">(</span><span style="color: #3366CC;">"Scriptable Tasks"</span><span style="color: #009900;">)</span>. <span style="color: #660066;">quit</span><span style="color: #009900;">(</span><span style="color: #009900;">)</span><span style="color: #339933;">;</span></pre>
    <p>
        点击
        <em>
            Run
        </em>
        ，应该可编写脚本的程序就退出了。改变脚本为下面的样子，并在此点击
        <em>
            Run
        </em>
        ：
    </p>
    <pre class="applescript" style="font-family:monospace;"><span style="color: #ff0033; font-weight: bold;">tell</span> <span style="color: #0066ff;">application</span> <span style="color: #009900;">"Scriptable Tasks"</span> <span style="color: #ff0033; font-weight: bold;">to</span> <span style="color: #0066ff;">launch</span></pre>
    <p>
        或
    </p>
    <pre class="javascript" style="font-family:monospace;">Application<span style="color: #009900;">(</span><span style="color: #3366CC;">"Scriptable Tasks"</span><span style="color: #009900;">)</span>.<span style="color: #660066;">launch</span><span style="color: #009900;">(</span><span style="color: #009900;">)</span><span style="color: #339933;">;</span></pre>
    <p>
        这个app会重新启动，但不会到达前台。要使它成为“焦点”，在上面的脚本改变
        <code>
            launch
        </code>
        为
        <code>
            activate
        </code>
        ，并单击
        <em>
            Run
        </em>
        。
    </p>
    <p>
        既然你已看到这个app可以响应脚本命令了，那就时候将这个能力添加到你的app上了。
    </p>
    <h2>
        让你的App可编写脚本
    </h2>
    <p>
        你的App的脚本定义文件定义了这个app可以做的事；这就有点像一个API。这个文件存在在你的app项目中，并指定了几件事情：
    </p>
    <ul>
        <li>
            标准的脚本对象和命令，例如
            <code>
                window
            </code>
            ，
            <code>
                make
            </code>
            ，
            <code>
                delete
            </code>
            ，
            <code>
                count
            </code>
            ，
            <code>
                open
            </code>
            和
            <code>
                quit
            </code>
            。
        </li>
        <li>
            你自己的可编写脚本的对象，属性和自定义命令。
        </li>
    </ul>
    <p>
        为了让你的app中的类可脚本化，你需要对其做出一些改变。
    </p>
    <p>
        首先，脚本的接口使用Key-Value-Coding来get和set对象的property。在OC中，所有的对象都自动地遵守KVC协议，但Swift的对象并不是这样的，除非你使其成为
        <code>
            NSObject
        </code>
        的子类。
    </p>
    <p>
        接下来，可脚本的类需要一个脚本接口可以识别的OC的名字。为了避免命名空间的冲突，Swift对象的名称是很难以给出一个独立的表示的。通过使用
        <code>
            @objc(YourClassName)
        </code>
        来给类添加前缀，你就给了它们一个可以被脚本引擎使用的名称。
    </p>
    <p>
        可编写脚本的类，需要对象说明符协助在应用或父对象中定位一个特定的对象，最终，这个app的delegate必须能够访问的到储存数据的地方，这样它才能返回应用的数据到脚本中。
    </p>
    <p>
        你并不必须从scratch来开始你自己的脚本定义文件，因为苹果提供了一个标注的SDEF文件供你使用。它就是
        <em>
            /System/Library/ScriptingDefinitions/
        </em>
        目录中的
        <em>
            CocoaStandard.sdef
        </em>
        文件。在Xcode中打开它并查看；它是XML格式的，带有指定的header，其中还有一个字典，里面是标准的套件。
    </p>
    <p>
        这时一个有用的起点，你
        This is a useful starting point, and you
        <i>
            可以
        </i>
        拷贝并粘贴这个XML到你自己的SDEF文件中。然而，从干净的代码的角度考量，让SDEF文件充满你的app不支持的命令和对象并不是一个好主意。因此，到了最后，这个示例工程应当只包含起始的SDEF文件移除了全部非必需记录的部分。
    </p>
    <p>
        关闭
        <em>
            CocoaStandard.sdef
        </em>
        并打开
        <em>
            ScriptableTasks.sdef
        </em>
        。在靠近结尾 
        <code>
            Insert Scriptable Tasks suite here
        </code>
        注释的这里添加下列代码：
    </p>
    <pre class="xml" style="font-family:monospace;"><span style="color: #808080; font-style: italic;">&lt;!-- 1 --&gt;</span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;suite</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">"Scriptable Tasks Suite"</span> <span style="color: #000066;">code</span>=<span style="color: #ff0000;">"ScTa"</span> <span style="color: #000066;">description</span>=<span style="color: #ff0000;">"Scriptable Tasks suite."</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
  <span style="color: #808080; font-style: italic;">&lt;!-- 2 --&gt;</span>
  <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;class</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">"application"</span> <span style="color: #000066;">code</span>=<span style="color: #ff0000;">"capp"</span> <span style="color: #000066;">description</span>=<span style="color: #ff0000;">"An application's top level scripting object."</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;cocoa</span> <span style="color: #000066;">class</span>=<span style="color: #ff0000;">"NSApplication"</span><span style="color: #000000; font-weight: bold;">/&gt;</span></span>
&nbsp;
    <span style="color: #808080; font-style: italic;">&lt;!-- 3 --&gt;</span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;element</span> <span style="color: #000066;">type</span>=<span style="color: #ff0000;">"task"</span> <span style="color: #000066;">access</span>=<span style="color: #ff0000;">"r"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;cocoa</span> <span style="color: #000066;">key</span>=<span style="color: #ff0000;">"tasks"</span><span style="color: #000000; font-weight: bold;">/&gt;</span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/element<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
  <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/class<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
&nbsp;
  <span style="color: #808080; font-style: italic;">&lt;!-- Insert command here --&gt;</span>
&nbsp;
  <span style="color: #808080; font-style: italic;">&lt;!-- 4 --&gt;</span>
  <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;class</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">"task"</span> <span style="color: #000066;">code</span>=<span style="color: #ff0000;">"TaSk"</span> <span style="color: #000066;">description</span>=<span style="color: #ff0000;">"A task item"</span> <span style="color: #000066;">inherits</span>=<span style="color: #ff0000;">"item"</span> <span style="color: #000066;">plural</span>=<span style="color: #ff0000;">"tasks"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;cocoa</span> <span style="color: #000066;">class</span>=<span style="color: #ff0000;">"Task"</span><span style="color: #000000; font-weight: bold;">/&gt;</span></span>
&nbsp;
      <span style="color: #808080; font-style: italic;">&lt;!-- 5 --&gt;</span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;property</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">"id"</span> <span style="color: #000066;">code</span>=<span style="color: #ff0000;">"ID  "</span> <span style="color: #000066;">type</span>=<span style="color: #ff0000;">"text"</span> <span style="color: #000066;">access</span>=<span style="color: #ff0000;">"r"</span></span>
<span style="color: #009900;">          <span style="color: #000066;">description</span>=<span style="color: #ff0000;">"The unique identifier of the task."</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
          <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;cocoa</span> <span style="color: #000066;">key</span>=<span style="color: #ff0000;">"id"</span><span style="color: #000000; font-weight: bold;">/&gt;</span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/property<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
&nbsp;
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;property</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">"name"</span> <span style="color: #000066;">code</span>=<span style="color: #ff0000;">"pnam"</span> <span style="color: #000066;">type</span>=<span style="color: #ff0000;">"text"</span> <span style="color: #000066;">access</span>=<span style="color: #ff0000;">"rw"</span></span>
<span style="color: #009900;">          <span style="color: #000066;">description</span>=<span style="color: #ff0000;">"The title of the task."</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
          <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;cocoa</span> <span style="color: #000066;">key</span>=<span style="color: #ff0000;">"title"</span><span style="color: #000000; font-weight: bold;">/&gt;</span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/property<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
&nbsp;
      <span style="color: #808080; font-style: italic;">&lt;!-- 6 --&gt;</span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;property</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">"daysUntilDue"</span> <span style="color: #000066;">code</span>=<span style="color: #ff0000;">"CrDa"</span> <span style="color: #000066;">type</span>=<span style="color: #ff0000;">"number"</span> <span style="color: #000066;">access</span>=<span style="color: #ff0000;">"rw"</span></span>
<span style="color: #009900;">      <span style="color: #000066;">description</span>=<span style="color: #ff0000;">"The number of days before this task is due."</span><span style="color: #000000; font-weight: bold;">/&gt;</span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;property</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">"completed"</span> <span style="color: #000066;">code</span>=<span style="color: #ff0000;">"TrFa"</span> <span style="color: #000066;">type</span>=<span style="color: #ff0000;">"boolean"</span> <span style="color: #000066;">access</span>=<span style="color: #ff0000;">"rw"</span></span>
<span style="color: #009900;">      <span style="color: #000066;">description</span>=<span style="color: #ff0000;">"Has the task been completed?"</span><span style="color: #000000; font-weight: bold;">/&gt;</span></span>
&nbsp;
      <span style="color: #808080; font-style: italic;">&lt;!-- 7 --&gt;</span>
      <span style="color: #808080; font-style: italic;">&lt;!-- Insert element of tags here --&gt;</span>
&nbsp;
      <span style="color: #808080; font-style: italic;">&lt;!-- Insert responds-to command here --&gt;</span>
&nbsp;
  <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/class<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
&nbsp;
  <span style="color: #808080; font-style: italic;">&lt;!-- Insert tag class here --&gt;</span>
&nbsp;
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/suite<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre>
    <p>
        这个XML的代码块做了很多的工作。一步一步来看：
    </p>
    <ol>
        <li>
            最外层的元素是
            <code>
                suite
            </code>
            ，所以你的SDEF文件现在有两个suite：
            <em>
                Standard Suite
            </em>
            和
            <em>
                Scriptable Tasks Suite
            </em>
            。在SDEF文件中的每件事都需要一个四字符的code。苹果的code几乎总是小写的，你将使用其中的几个用于特定的目的。对于你自己的suite，class和property，则最好使用大写、小写和符号的随机混合来避免冲突。
        </li>
        <li>
            下一部分定义了应用，并必须使用code值
            <code>
                "capp"
            </code>
            。你必须制定application的class；如果你子类化了
            <code>
                NSApplication
            </code>
            ，你就该在这里使用你子类的名称了。
        </li>
        <li>
            这个application包含
            <code>
                element
            </code>
            。在这个app中，element被储存在app的delegate，一个叫做
            <code>
                tasks
            </code>
            的数组中。在脚本术语中，element是app和其它对象可以包含的对象。
        </li>
        <li>
            最后的一个块定义了application包含的
            <code>
                Task
            </code>
            class。访问多个的复数名称是
            <code>
                tasks
            </code>
            。在这个app中，支持这个对象类型的class是
            <code>
                Task
            </code>
            。
        </li>
        <li>
            前两个property是特定的。请看它们的code：
            <code>
                "ID "
            </code>
            an和d
            <code>
                "pnam"
            </code>
            。
            <code>
                "ID "
            </code>
            （注意字母之后的两个空格）指定了这个对象的唯一标识符。
            <code>
                "pnam"
            </code>
            指定了这个对象的
            <code>
                name
            </code>
            property。你可以使用它们中的任一个，来直接访问对象。
            <p>
                <code>
                    "ID "
                </code>
                是只读的，因为脚本不应该改变唯一标识符，但
                <code>
                    "pnam"
                </code>
                是可读写的。它们都是text类型的property。
                <code>
                    "pnam"
                </code>
                property映射到了
                <code>
                    Task
                </code>
                对象的
                <code>
                    title
                </code>
                property。
            </p>
        </li>
        <li>
            还剩两个property，一个是number类型的property
            <code>
                daysUntilDue
            </code>
            ，另一个是Boolean类型的property
            <code>
                completed
            </code>
            。它们可以在对象和脚本中使用相同的名称，因此你不需要指定
            <code>
                cocoa key
            </code>
            。
        </li>
        <li>
            “Insert…”的注释是为你需要添加更多内容到这个文件时的占位符。
        </li>
    </ol>
    <p>
        打开
        <em>
            Info.plist
        </em>
        ，在记录下方的空白处右击，并选择
        <em>
            Add Row
        </em>
        。输入一个大写的
        <em>
            S
        </em>
        ，将建议的列别滚动到
        <em>
            Scriptable
        </em>
        。选择它并将设置更改为
        <em>
            YES
        </em>
        。
    </p>
    <p>
        重复这个过程来选择下一项：
        <em>
            Scripting definition file name
        </em>
        。设置它为你的SDEF文件的文件名：
        <em>
            ScriptableTasks.sdef
        </em>
    </p>
    <p>
        如果你喜欢以源码的形式编辑Info.plist，你也可以添加下列的记录到主字典中：
    </p>
    <pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;key<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>NSAppleScriptEnabled<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/key<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;true</span><span style="color: #000000; font-weight: bold;">/&gt;</span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;key<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>OSAScriptingDefinition<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/key<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;string<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>ScriptableTasks.sdef<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/string<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre>
    <p>
        现在你必须修改app的delegate，来处理从脚本中传来的请求。
    </p>
    <p>
        打开
        <em>
            AppDelegate.swift
        </em>
        文件，并添加下列代码到文件的尾部：
    </p>
    <pre class="swift" style="font-family:monospace;">extension AppDelegate {
  // 1
  override func application(_ sender: NSApplication, delegateHandlesKey key: String) -&gt; Bool {
    return key == "tasks"
  }
&nbsp;
  // 2
  func insertObject(_ object: Task, inTasksAtIndex index: Int) {
    tasks = dataProvider.insertNew(task: object, at: index)
  }
&nbsp;
  func removeObjectFromTasksAtIndex(_ index: Int) {
    tasks = dataProvider.deleteTask(at: index)
  }
}</pre>
    <p>
        上面的代码执行了以下的事：
    </p>
    <ol>
        <li>
            当一个脚本请求
            <code>
                tasks
            </code>
            的数据时，这个方法将确认app的delegate可以处理它。
        </li>
        <li>
            如果一个脚本尝试插入，编辑或删除数据，这些方法将传递那些请求到
            <code>
                dataProvider
            </code>
            中。
        </li>
    </ol>
    <p>
        为了使
        <code>
            Task
        </code>
        的model类对脚本可用，你必须在做一点coding。
    </p>
    <p>
        打开
        <em>
            Task.swift
        </em>
        ，并将类的定义修改成下面的样子：
    </p>
    <pre class="swift" style="font-family:monospace;">@objc(Task) class Task: NSObject {</pre>
    <p>
        Xcode会立刻抱怨说
        <code>
            init
        </code>
        要求
        <code>
            override
        </code>
        关键字，所以让Fix-It来做吧。这是必需的，因为这个类现在有一个父类：
    </p>
    <pre class="swift" style="font-family:monospace;">override init() {</pre>
    <p>
        <em>
            Task.swift
        </em>
        需要更多的修改：一个对象说明符。插入下列的方法到
        <code>
            Task
        </code>
        的类中：
    </p>
    <pre class="swift" style="font-family:monospace;">override var objectSpecifier: NSScriptObjectSpecifier {
  // 1
  let appDescription = NSApplication.shared().classDescription as! NSScriptClassDescription
&nbsp;
  // 2
  let specifier = NSUniqueIDSpecifier(containerClassDescription: appDescription,
                                      containerSpecifier: nil, key: "tasks", uniqueID: id)
  return specifier
}</pre>
    <p>
        以此来对每个编号评论：
    </p>
    <ol>
        <li>
            因为app是task的容器，获取app的类的描述。
        </li>
        <li>
            通过id在app中获取任务的描述。这就是为什么Task类有一个
            <code>
                id
            </code>
            的property - 这样每个任务就可以被正确地指定。
        </li>
    </ol>
    <p>
        你终于可以开始脚本化你的app了！
    </p>
    <h2>
        脚本化你的App
    </h2>
    <p>
        在你开始之前，确保退出任何这个app运行中的实例，它们可能是被Script Editor打开的。
    </p>
    <p>
        运行Scriptable Task；右击Dock上的icon，并在Finder中选择
        <em>
            Options/Show
        </em>
        。退出
        <em>
            Script Editor
        </em>
        app并重启，让它对你的app做出的改变生效。
    </p>
    <p>
        打开
        <em>
            Library
        </em>
        的window，并从
        <em>
            Finder
        </em>
        中拖拽
        <em>
            Scriptable Tasks
        </em>
        到
        <em>
            Library
        </em>
        window中。
    </p>
    <p>
        如果你收到了一个错误，说这个app是不可编写脚本的，尝试退出Script Editor并重启它，因为它有时没有注册一个新build的app。如果它仍然没能成功地导入，请返回并仔细检查你对SDEF文件进行的修改。
    </p>
    <p>
        双击Library中的
        <em>
            Scriptable Tasks
        </em>
        来查看app的字典：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/ScriptableTasksDictionary1.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/04/ScriptableTasksDictionary1-700x458.png"
            alt="Making a mac app scriptable tutorial: Scriptable Tasks Dictionary 1"
            width="700" height="458" class="aligncenter size-large wp-image-133012"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/04/ScriptableTasksDictionary1.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/04/ScriptableTasksDictionary1-480x314.png 480w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        你将看到Standard Suite和Scriptable Tasks Suite。单击
        <em>
            Scriptable Tasks
        </em>
        suite，你将看到你在SDEF文件中添加了什么。这个应用包含任务，一个任务包含四个property。
    </p>
    <p>
        使用工具栏中的
        <em>
            Language
        </em>
        弹出菜单，来改变目录中的脚本语言为
        <em>
            JavaScript
        </em>
        。你将看到基本相同的信息，但有一个重要的变化。class和property的case发生了改变。我不清楚这是因为什么，但他是那些你需要注意的“陷阱（gotchas）”之一。
    </p>
    <p>
        在
        <em>
            Script Editor
        </em>
        中，创建一个新的脚本文件，并设置这个编辑器展示
        <em>
            Log/Replies
        </em>
        。测试下面的脚本之一，确保在语言的弹出菜单中选择恰当的语言：
    </p>
    <pre class="applescript" style="font-family:monospace;"><span style="color: #ff0033; font-weight: bold;">tell</span> <span style="color: #0066ff;">application</span> <span style="color: #009900;">"Scriptable Tasks"</span>
  <span style="color: #ff0033; font-weight: bold;">get</span> <span style="color: #ff0033;">every</span> task
<span style="color: #ff0033; font-weight: bold;">end</span> <span style="color: #ff0033; font-weight: bold;">tell</span></pre>
    <p>
        或
    </p>
    <pre class="javascript" style="font-family:monospace;">app <span style="color: #339933;">=</span> Application<span style="color: #009900;">(</span><span style="color: #3366CC;">"Scriptable Tasks"</span><span style="color: #009900;">)</span><span style="color: #339933;">;</span>
app.<span style="color: #660066;">tasks</span><span style="color: #009900;">(</span><span style="color: #009900;">)</span><span style="color: #339933;">;</span></pre>
    <p>
        在log中，你将看到一个通过ID的task的列表。为了让信息更有用，编辑脚本就像下面这样：
    </p>
    <pre class="applescript" style="font-family:monospace;"><span style="color: #ff0033; font-weight: bold;">tell</span> <span style="color: #0066ff;">application</span> <span style="color: #009900;">"Scriptable Tasks"</span>
  <span style="color: #ff0033; font-weight: bold;">get</span> <span style="color: #ff0033;">the</span> <span style="color: #0066ff;">name</span> <span style="color: #ff0033; font-weight: bold;">of</span> <span style="color: #ff0033;">every</span> task
<span style="color: #ff0033; font-weight: bold;">end</span> <span style="color: #ff0033; font-weight: bold;">tell</span></pre>
    <p>
        或
    </p>
    <pre class="javascript" style="font-family:monospace;">app <span style="color: #339933;">=</span> Application<span style="color: #009900;">(</span><span style="color: #3366CC;">"Scriptable Tasks"</span><span style="color: #009900;">)</span><span style="color: #339933;">;</span>
app.<span style="color: #660066;">tasks</span>.<span style="color: #000066;">name</span><span style="color: #009900;">(</span><span style="color: #009900;">)</span><span style="color: #339933;">;</span></pre>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/AppleScriptTasks.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/04/AppleScriptTasks-482x500.png"
            alt="Making a mac app scriptable tutorial: AppleScript Tasks" width="482"
            height="500" class="aligncenter size-large wp-image-133015" srcset="https://koenig-media.raywenderlich.com/uploads/2016/04/AppleScriptTasks-482x500.png 482w, https://koenig-media.raywenderlich.com/uploads/2016/04/AppleScriptTasks-309x320.png 309w, https://koenig-media.raywenderlich.com/uploads/2016/04/AppleScriptTasks-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2016/04/AppleScriptTasks.png 700w"
            sizes="(max-width: 482px) 100vw, 482px">
        </a>
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/JavaScriptTasks.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/04/JavaScriptTasks-479x500.png"
            alt="Making a mac app scriptable tutorial: JavaScript Tasks" width="479"
            height="500" class="aligncenter size-large wp-image-133016" srcset="https://koenig-media.raywenderlich.com/uploads/2016/04/JavaScriptTasks-479x500.png 479w, https://koenig-media.raywenderlich.com/uploads/2016/04/JavaScriptTasks-307x320.png 307w, https://koenig-media.raywenderlich.com/uploads/2016/04/JavaScriptTasks-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2016/04/JavaScriptTasks.png 700w"
            sizes="(max-width: 479px) 100vw, 479px">
        </a>
    </p>
    <p>
        再尝试一些你之前下载的脚本。当运行脚本的时候，确保你将Script Editor设置为
        <em>
            Log/Replies
        </em>
        这样你就能一路上看到结果。
    </p>
    <p>
        每个脚本在重写运行它之前退出这个app；这是为了在任何的编辑之后重置数据，这样示例脚本就如同期望一般地工作。你通常不会在你自己的脚本中执行此操作。
    </p>
    <div class="note">
        <p>
            <em>
                注意：
            </em>
            Script Editor会在你build更新版本的app时感到非常困惑，因为如果你有一个打开的正在使用这个app的脚本，它会尝试一直保持其同一版本来运行。这通常会以app的老版本形式结束，因此在每次build之前，退出app。
        </p>
        <p>
            任何时候，如果你看到两个副本的Scriptable Tasks的app正在运行，或在任何示例中出现了脚本的错误，你可以确定，这是Script Editor已跑在了错误版本的app上。最简单的修复就是退出所有副本的app，并退出Script Editor。Clean Xcode的build（
            <em>
                Product/Clean
            </em>
            ），然后build并再次运行。
        </p>
        <p>
            重新启动Script Editor，当它打开脚本的时候，单击
            <em>
                Compile
            </em>
            ，然后单击
            <em>
                Run
            </em>
            。如果失败了的话，请在
            <em>
                ~/Library/Developer/Xcode/DerivedData
            </em>
            里删除app中的Derived Data。
        </p>
    </div>
    <p>
        尝试下面的两个示例脚本：
    </p>
    <p>
        <em>
            3. 获取Tasks.scpt
        </em>
    </p>
    <p>
        这个脚本使用各种过滤器检索任务的数量和任务的名称。记下下列事项：
    </p>
    <ul>
        <li>
            JavaScript从0开始计数，而AppleScript从1开始计数。
        </li>
        <li>
            文本搜索是不区分大小写的。
        </li>
    </ul>
    <p>
        <em>
            4. 添加编辑Tasks.scpt
        </em>
    </p>
    <p>
        这个脚本添加了新的任务，在第一个任务上切换了
        <code>
            completed
        </code>
        的标记，并尝试创建另一个相同名称的任务。
    </p>
    <p>
        嗯...创建一个同名的任务work了！现在你有了两个”喂猫“的任务。猫会很激动，但对于这个app的目的，任务的名称应当是唯一的。尝试添加一个名称早已存在的任务可能产生一个错误。
    </p>
    <p>
        回到
        <em>
            Xcode
        </em>
        ，查看
        <em>
            AppDelegate.swift
        </em>
        ，你会看到当脚本想要插入一个对象时，app的delegate会将这个调用床底给
        <code>
            dataProvider
        </code>
        。在
        <em>
            DataProvider.swift
        </em>
        中，查看
        <code>
            insertNew(task:at:)
        </code>
        ，它将一个存在的任务插入到数组中，或添加了一个新的任务到结尾。
    </p>
    <p>
        到了在这里添加一次检查的时候了。用下列的代码来替换这个方法：
    </p>
    <pre class="swift" style="font-family:monospace;">mutating func insertNew(task: Task, at index: Int) -&gt; [Task] {
  // 1
  if taskExists(withTitle: task.title) {
    // 2
    let command = NSScriptCommand.current()
    command?.scriptErrorNumber = errOSACantAssign
    command?.scriptErrorString = "Task with the title '\(task.title)' already exists"
  } else {
    // 3
    if index &gt;= tasks.count {
      tasks.append(task)
    } else {
      tasks.insert(task, at: index)
    }
&nbsp;
    postNotificationOfChanges()
  }
&nbsp;
  return tasks
}</pre>
    <p>
        这里是每条评论处所做的事：
    </p>
    <ol>
        <li>
            使用现有的函数来检查是否这个名称的任务早已存在。
        </li>
        <li>
            如果这个名称
            <i>
                不是
            </i>
            唯一的：
            <ul>
                <li>
                    获取对调用这个函数的脚本命令的引用。
                </li>
                <li>
                    查看命令的
                    <code>
                        errorNumber
                    </code>
                    和
                    <code>
                        errorString
                    </code>
                    property；
                    <code>
                        errOSACantAssign
                    </code>
                    是AppleScript的标准错误码之一。这些将被发送回调用的脚本。
                </li>
            </ul>
        </li>
        <li>
            如果这个名称是
            <i>
                是
            </i>
            唯一的：
            <ul>
                <li>
                    像之前一样地处理任务。
                </li>
                <li>
                    发送数据变化的通知。ViewController会看到这个并更新展示。
                </li>
            </ul>
        </li>
    </ol>
    <p>
        如果app正在运行，退出，然后运行你的app。再次运行
        <em>
            4. 添加Edit Tasks
        </em>
        脚本。这次你应当会得到一个错误的对话框，而不是创建副本的任务。对不起，猫...
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/04/hungry_cat.png"
        alt="Making a mac app scriptable tutorial: Hungry Cat" width="400" height="445"
        class="aligncenter size-full wp-image-133079" srcset="https://koenig-media.raywenderlich.com/uploads/2016/04/hungry_cat.png 400w, https://koenig-media.raywenderlich.com/uploads/2016/04/hungry_cat-288x320.png 288w"
        sizes="(max-width: 400px) 100vw, 400px">
    </p>
    <p>
        <em>
            5. 删除Tasks.scpt
        </em>
    </p>
    <p>
        这个脚步删除了一个任务，检查是否存在一个特定的任务，并删除它，最终删除全部完成的任务。
    </p>
    <h2>
        使用嵌入的（Nested）对象
    </h2>
    <p>
        在示例的app中，第二列展示了一个，分配给每项任务的标签的列表。到目前为止，你仍然没有办法通过脚本来使用它们 - 是时候来修复这个了！
    </p>
    <p>
        对象的说明符可以处理对象的层次结构。这是你在这里拥有的，而应用程序拥有着任务，并且任务拥有它的标签。
    </p>
    <p>
        与
        <code>
            Task
        </code>
        类一样，你需要使
        <code>
            Tag
        </code>
        脚本化。
    </p>
    <p>
        打开
        <em>
            Tag.swift
        </em>
        ，并作出下面的变化：
    </p>
    <ul>
        <li>
            将类的定义这行修改为：
            <code>
                @objc(Tag) class Tag: NSObject {
            </code>
        </li>
        <li>
            添加
            <code>
                override
            </code>
            关键字到
            <code>
                init
            </code>
            上。
        </li>
        <li>
            添加对象说明符的方法：
        </li>
    </ul>
    <pre class="swift" style="font-family:monospace;">override var objectSpecifier: NSScriptObjectSpecifier {
  // 1
  guard let task = task else { return NSScriptObjectSpecifier() }
&nbsp;
  // 2
  guard let taskClassDescription = task.classDescription as? NSScriptClassDescription else {
    return NSScriptObjectSpecifier()
  }
&nbsp;
  // 3
  let taskSpecifier = task.objectSpecifier
&nbsp;
  // 4
  let specifier = NSUniqueIDSpecifier(containerClassDescription: taskClassDescription,
    containerSpecifier: taskSpecifier, key: "tags", uniqueID: id)
  return specifier
}</pre>
    <p>
        上面的代码相对是比较简单的：
    </p>
    <ol>
        <li>
            检查标签是否具有分配的任务。
        </li>
        <li>
            检查任务是否具有正确的类的类描述。
        </li>
        <li>
            获取父任务的对象说明符。
        </li>
        <li>
            为包含在任务中的标签，构建对象说明符，并返回。
        </li>
    </ol>
    <p>
        在评论 
        <code>
            Insert tag class here
        </code>
        处，添加下列的代码到SDEF文件中：
    </p>
    <pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;class</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">"tag"</span> <span style="color: #000066;">code</span>=<span style="color: #ff0000;">"TaGg"</span> <span style="color: #000066;">description</span>=<span style="color: #ff0000;">"A tag"</span> <span style="color: #000066;">inherits</span>=<span style="color: #ff0000;">"item"</span> <span style="color: #000066;">plural</span>=<span style="color: #ff0000;">"tags"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
  <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;cocoa</span> <span style="color: #000066;">class</span>=<span style="color: #ff0000;">"Tag"</span><span style="color: #000000; font-weight: bold;">/&gt;</span></span>
  <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;property</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">"id"</span> <span style="color: #000066;">code</span>=<span style="color: #ff0000;">"ID  "</span> <span style="color: #000066;">type</span>=<span style="color: #ff0000;">"text"</span> <span style="color: #000066;">access</span>=<span style="color: #ff0000;">"r"</span></span>
<span style="color: #009900;">    <span style="color: #000066;">description</span>=<span style="color: #ff0000;">"The unique identifier of the tag."</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;cocoa</span> <span style="color: #000066;">key</span>=<span style="color: #ff0000;">"uniqueID"</span><span style="color: #000000; font-weight: bold;">/&gt;</span></span>
  <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/property<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
  <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;property</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">"name"</span> <span style="color: #000066;">code</span>=<span style="color: #ff0000;">"pnam"</span> <span style="color: #000066;">type</span>=<span style="color: #ff0000;">"text"</span> <span style="color: #000066;">access</span>=<span style="color: #ff0000;">"rw"</span></span>
<span style="color: #009900;">    <span style="color: #000066;">description</span>=<span style="color: #ff0000;">"The name of the tag."</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;cocoa</span> <span style="color: #000066;">key</span>=<span style="color: #ff0000;">"name"</span><span style="color: #000000; font-weight: bold;">/&gt;</span></span>
  <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/property<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/class<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre>
    <p>
        它和
        <code>
            Task
        </code>
        class的数据非常相似，但一个标签只有两个暴露的property：
        <code>
            id
        </code>
        和
        <code>
            name
        </code>
        。
    </p>
    <p>
        现在必须要对
        <code>
            Task
        </code>
        部分进行一下编辑，来指出它包含着tag元素了。
    </p>
    <p>
        添加下列的代码到Task类的XML中，在
        <code>
            Insert element of tags here
        </code>
        的注释处：
    </p>
    <pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;element</span> <span style="color: #000066;">type</span>=<span style="color: #ff0000;">"tag"</span> <span style="color: #000066;">access</span>=<span style="color: #ff0000;">"rw"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
  <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;cocoa</span> <span style="color: #000066;">key</span>=<span style="color: #ff0000;">"tags"</span><span style="color: #000000; font-weight: bold;">/&gt;</span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/element<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre>
    <p>
        退出app，然后再次运行。
    </p>
    <p>
        返回
        <em>
            Script Editor
        </em>
        ；如果
        <em>
            Scriptable Tasks dictionary
        </em>
        已打开，就关闭并重新打开它。观察它是否包含关于标签的信息。
    </p>
    <p>
        如果不存在，就从
        <em>
            Library
        </em>
        中移除
        <em>
            Scriptable Tasks
        </em>
        记录并在此添加，通过将app拖拽到window中：        
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/ScriptableTasksDictionary2.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/04/ScriptableTasksDictionary2-617x500.png"
            alt="Making a mac app scriptable tutorial: Scriptable Tasks Dictionary 2"
            width="617" height="500" class="aligncenter size-large wp-image-133013"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/04/ScriptableTasksDictionary2-617x500.png 617w, https://koenig-media.raywenderlich.com/uploads/2016/04/ScriptableTasksDictionary2-395x320.png 395w, https://koenig-media.raywenderlich.com/uploads/2016/04/ScriptableTasksDictionary2.png 700w"
            sizes="(max-width: 617px) 100vw, 617px">
        </a>
    </p>
    <p>
        尝试下列脚本中的一个：
    </p>
    <pre class="applescript" style="font-family:monospace;"><span style="color: #ff0033; font-weight: bold;">tell</span> <span style="color: #0066ff;">application</span> <span style="color: #009900;">"Scriptable Tasks"</span>
  <span style="color: #ff0033; font-weight: bold;">get</span> <span style="color: #ff0033;">the</span> <span style="color: #0066ff;">name</span> <span style="color: #ff0033; font-weight: bold;">of</span> <span style="color: #ff0033;">every</span> tag <span style="color: #ff0033; font-weight: bold;">of</span> task <span style="color: #000000;">1</span>
<span style="color: #ff0033; font-weight: bold;">end</span> <span style="color: #ff0033; font-weight: bold;">tell</span></pre>
    <p>
        或
    </p>
    <pre class="javascript" style="font-family:monospace;">app <span style="color: #339933;">=</span> Application<span style="color: #009900;">(</span><span style="color: #3366CC;">"Scriptable Tasks"</span><span style="color: #009900;">)</span><span style="color: #339933;">;</span>
app.<span style="color: #660066;">tasks</span><span style="color: #009900;">[</span><span style="color: #CC0000;">0</span><span style="color: #009900;">]</span>.<span style="color: #660066;">tags</span>.<span style="color: #000066;">name</span><span style="color: #009900;">(</span><span style="color: #009900;">)</span><span style="color: #339933;">;</span></pre>
    <p>
        现在你可以在app中检索tag了 - 但添加一些新的怎么样？
    </p>
    <p>
        你可能会注意到在
        <em>
            Tag.swift
        </em>
        中，每个
        <code>
            Tag
        </code>
        都有一个弱引用指向它自己的任务。当获取了对象说明符后，它可以帮助创建连接，因此当分配一个熄灯tag到任务中时，任务的property必须被设置。
    </p>
    <p>
        打开
        <em>
            Task.swift
        </em>
        并添加下列的方法到
        <code>
            Task
        </code>
        的类中：
    </p>
    <pre class="swift" style="font-family:monospace;">override func newScriptingObject(of objectClass: AnyClass,
                                 forValueForKey key: String,
                                 withContentsValue contentsValue: Any?,
                                 properties: [String: Any]) -&gt; Any? {
&nbsp;
  let tag: Tag = super.newScriptingObject(of: objectClass, forValueForKey: key,
                                          withContentsValue: contentsValue,
                                          properties: properties) as! Tag
  tag.task = self
&nbsp;
  return tag
}</pre>
    <p>
        为什么你将它放到 
        <code>
            Task
        </code>
        类而不是
        <code>
            Tag
        </code>
        类中，是因为这个方法被发送到了新对象的容器中。这个调用被传递到了
        <code>
            父类
        </code>
        中来获取新的标签，然后这个task的property就被赋值了。
    </p>
    <p>
        退出。再次运行你的app。现在运行示例的脚本
        <em>
            6. Tasks With Tags.scpt
        </em>
        ，它列出标签的名称，通过指定的标签列出任务，并可以删除和创建tag。
    </p>
    <h2>
        添加定制的命令
    </h2>
    <p>
        当制作一个app脚本时，你还可以采取一步：添加定制的命令。在之前的脚本中，你直接切换了任务的
        <code>
            completed
        </code>
        标记。但难道不应该更好一些 - 更安全一些么？能否可以使用一个命令来完成，而不是直接改变property？
    </p>
    <p>
        考虑下列的脚本：
    </p>
    <pre class="applescript" style="font-family:monospace;">mark <span style="color: #ff0033;">the</span> <span style="color: #ff0033;">first</span> task <span style="color: #ff0033;">as</span> <span style="color: #009900;">"done"</span>
mark task <span style="color: #009900;">"Feed the cat"</span> <span style="color: #ff0033;">as</span> <span style="color: #009900;">"not done"</span></pre>
    <p>
        我相信你已达到了SDEF文件，你完成的是正确的：这个命令必须首先被定义。
    </p>
    <p>
        这里需要两个步骤：
    </p>
    <ol>
        <li>
            告诉应用这个命令存在，和它的参数是什么。
        </li>
        <li>
            告诉Task类它响应命令，以及要调用的方法来实现它。
        </li>
    </ol>
    <p>
        在Scriptable Tasks suite中，所有的类之外，在
        <em>
            Insert command here
        </em>
        注释中，添加下列的代码：
    </p>
    <pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;command</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">"mark"</span> <span style="color: #000066;">code</span>=<span style="color: #ff0000;">"TaSktext"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
  <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;direct-parameter</span> <span style="color: #000066;">description</span>=<span style="color: #ff0000;">"One task"</span> <span style="color: #000066;">type</span>=<span style="color: #ff0000;">"task"</span><span style="color: #000000; font-weight: bold;">/&gt;</span></span>
  <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;parameter</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">"as"</span> <span style="color: #000066;">code</span>=<span style="color: #ff0000;">"DFLG"</span> <span style="color: #000066;">description</span>=<span style="color: #ff0000;">"'done' or 'not done'"</span> <span style="color: #000066;">type</span>=<span style="color: #ff0000;">"text"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;cocoa</span> <span style="color: #000066;">key</span>=<span style="color: #ff0000;">"doneFlag"</span><span style="color: #000000; font-weight: bold;">/&gt;</span></span>
  <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/parameter<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/command<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre>
    <p>
        “等一下！“你说。“之前你说code必须是
        <i>
            四个
        </i>
        字符，但现在我有了一个八个字符的？这里发生了什么？”
    </p>
    <p>
        当定义一个方法的时候，你提供一个两个部分的code。它组合了参数的code或类型 - 在这个case中是一个
        <code>
            Task
        </code>
        对象和一些文本。
    </p>
    <p>
        在
        <code>
            Task
        </code>
        类的定义中，
        <em>
            Insert responds-to command here
        </em>
        的注释处，添加下列代码：
    </p>
    <pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;responds-to</span> <span style="color: #000066;">command</span>=<span style="color: #ff0000;">"mark"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
  <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;cocoa</span> <span style="color: #000066;">method</span>=<span style="color: #ff0000;">"markAsDone:"</span><span style="color: #000000; font-weight: bold;">/&gt;</span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/responds-to<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre>
    <p>
        现在返回
        <em>
            Task.swift
        </em>
        并添加下列代码：
    </p>
    <pre class="swift" style="font-family:monospace;">func markAsDone(_ command: NSScriptCommand) {
  if let task = command.evaluatedReceivers as? Task,
    let doneFlag = command.evaluatedArguments?["doneFlag"] as? String {
    if self == task {
      if doneFlag == "done" {
        completed = true
      } else if doneFlag == "not done" {
        completed = false
      }
      // if doneFlag doesn't match either string, leave un-changed
    }
  }
}</pre>
    <p>
        <code>
            markAsDone(\_:)
        </code>
        的参数是
        <code>
            NSScriptCommand
        </code>
        类型的，它含有两个有用的property：
        <code>
            evaluatedReceivers
        </code>
        和
        <code>
            evaluatedArguments
        </code>
        。从它们这里，你会尝试获取任务和字符创的参数，并使用它们来调整相应的任务。
    </p>
    <p>
        退出，再次运行你的app。在Script Editor中查看字典，如果
        <code>
            mark
        </code>
        命令未显示，请删除并重新导入它：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/ScriptableTasksDictionary3.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/04/ScriptableTasksDictionary3-593x500.png"
            alt="Making a mac app scriptable tutorial: Scriptable Tasks Dictionary 3"
            width="593" height="500" class="aligncenter size-large wp-image-133014"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/04/ScriptableTasksDictionary3-593x500.png 593w, https://koenig-media.raywenderlich.com/uploads/2016/04/ScriptableTasksDictionary3-380x320.png 380w, https://koenig-media.raywenderlich.com/uploads/2016/04/ScriptableTasksDictionary3.png 700w"
            sizes="(max-width: 593px) 100vw, 593px">
        </a>
    </p>
    <p>
        现在，你应该可以运行
        <em>
            7. Custom Command.scpt
        </em>
        脚本，并看到你的新的脚本正在执行中了。
    </p>
    <div class="note">
        <em>
            注意：
        </em>
        Swift 3改变了命令发送到对象中的方式。AppleScript仍会按照预期一般地工作，但
        <code>
            mark
        </code>
        命令在JavaScript中却失效了。我已经添加了
        <code>
            completed
        </code>
        property的手动切换到JavaScript版本的
        <em>
            7. Custom Command.scpt
        </em>
        中，但也在这里留下了原来的版本。希望它可以在Swift更新之后生效。
    </div>
    <h2>
        从这儿去哪里？
    </h2>
    <div class="inline-video-ad" id="sub-banner-inline">
        <div class="inline-video-ad-wrapper">
            <a href="https://videos.raywenderlich.com/courses">
                <div class="col-wrapper">
                    <div class="col">
                        <img src="https://koenig-assets.raywenderlich.com/wp-content/themes/raywenderlich/images/global/video-yeti@2x.png"
                        alt="yeti holding videos">
                    </div>
                    <div class="col large-col">
                        <span>
                            想要学习得更快？通过我们的
                            <span>
                                视频课程
                            </span>
                            来节约时间吧
                        </span>
                    </div>
                </div>
            </a>
        </div>
    </div>
    <p>
        你可以在
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/07/ScriptableTasks-Final2.zip">
            这里
        </a>
        下载最终版本的示例项目。
    </p>
    <p>
        在这个mac app的可脚本化的教程中，没有覆盖到app间的通信。对于如何在app之间工作，请访问
        <em>
            8. Inter-App Communication.scpt
        </em>
        来查看一些例子。这个例子收集了今天和明天未完成的任务，并将它们插入到了一个新的TextEdit文件，样式化文本并保存文件。
    </p>
    <p>
        对于可执行脚本app的更多信息，苹果官方的文档在这里
        <a href="https://developer.apple.com/library/mac/documentation/AppleScript/Conceptual/AppleScriptX/Concepts/scriptable_apps.html">
            Scriptable Applications
        </a>
        ，它是一个很好的开始，苹果的
        <a href="https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/ScriptableCocoaApplications/SApps_about_apps/SAppsAboutApps.html#//apple_ref/doc/uid/TP40001976">
            Overview of Cocoa Support for Scriptable Applications
        </a>
        也是这样。
    </p>
    <p>
        感兴趣于了解更多的JXA？请访问
        <a href="https://developer.apple.com/library/mac/releasenotes/InterapplicationCommunication/RN-JavaScriptForAutomation/Articles/Introduction.html">
            Introduction to JavaScript for Automation Release Notes
        </a>
        。
    </p>
</div>