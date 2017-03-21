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
        ，在Xcode中打开它，build并运行，查看它的样子：
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
        Every scriptable app has a dictionary, stored in a scripting definition
        (SDEF) file. The dictionary tells you what objects the app has, what properties
        the objects have and what commands the app responds to. In the above screen
        shot, you can see that TextEdit has paragraphs, and paragraphs have color
        and font properties. You will use this information to style some text.
    </p>
    <p>
        Open
        <em>
            1. TextEdit Write.scpt
        </em>
        from either the
        <em>
            AppleScript
        </em>
        or the
        <em>
            JavaScript
        </em>
        folder. Run the script; you’ll see TextEdit create and save a document.
    </p>
    <p>
        You now have a new document, but it needs a bit of styling. Open
        <em>
            2. TextEdit Read Edit.scpt
        </em>
        , run this script and you’ll see the document re-opened and styled as
        per the script.
    </p>
    <p>
        Although delving into the actual script is beyond the scope of this tutorial,
        feel free to read the scripts in detail to see how they act on the TextEdit
        document.
    </p>
    <p>
        As mentioned in the introduction, all apps are scriptable to some extent.
        To see this in action, ensure Scriptable Tasks is running. Next, open a
        new script window in Script Editor and enter one of the following scripts,
        depending on which language you’re using:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1330071">
                    <td class="code" id="p133007code1">
                        <pre class="applescript" style="font-family:monospace;">
                            <span style="color: #808080; font-style: italic;">
                                -- AppleScript
                            </span>
                            <span style="color: #ff0033; font-weight: bold;">
                                tell
                            </span>
                            <span style="color: #0066ff;">
                                application
                            </span>
                            <span style="color: #009900;">
                                "Scriptable Tasks"
                            </span>
                            <span style="color: #ff0033; font-weight: bold;">
                                to
                            </span>
                            <span style="color: #0066ff;">
                                quit
                            </span>
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        or
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1330072">
                    <td class="code" id="p133007code2">
                        <pre class="javascript" style="font-family:monospace;">
                            <span style="color: #006600; font-style: italic;">
                                // JavaScript
                            </span>
                            Application
                            <span style="color: #009900;">
                                (
                            </span>
                            <span style="color: #3366CC;">
                                "Scriptable Tasks"
                            </span>
                            <span style="color: #009900;">
                                )
                            </span>
                            .
                            <span style="color: #660066;">
                                quit
                            </span>
                            <span style="color: #009900;">
                                (
                            </span>
                            <span style="color: #009900;">
                                )
                            </span>
                            <span style="color: #339933;">
                                ;
                            </span>
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Click
        <em>
            Run
        </em>
        and Scriptable Tasks should quit. Change the script to the following and
        click
        <em>
            Run
        </em>
        again:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1330073">
                    <td class="code" id="p133007code3">
                        <pre class="applescript" style="font-family:monospace;">
                            <span style="color: #ff0033; font-weight: bold;">
                                tell
                            </span>
                            <span style="color: #0066ff;">
                                application
                            </span>
                            <span style="color: #009900;">
                                "Scriptable Tasks"
                            </span>
                            <span style="color: #ff0033; font-weight: bold;">
                                to
                            </span>
                            <span style="color: #0066ff;">
                                launch
                            </span>
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        or
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1330074">
                    <td class="code" id="p133007code4">
                        <pre class="javascript" style="font-family:monospace;">
                            Application
                            <span style="color: #009900;">
                                (
                            </span>
                            <span style="color: #3366CC;">
                                "Scriptable Tasks"
                            </span>
                            <span style="color: #009900;">
                                )
                            </span>
                            .
                            <span style="color: #660066;">
                                launch
                            </span>
                            <span style="color: #009900;">
                                (
                            </span>
                            <span style="color: #009900;">
                                )
                            </span>
                            <span style="color: #339933;">
                                ;
                            </span>
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        The app restarts, but doesn’t come to the foreground. To bring the app
        into focus, change
        <code>
            launch
        </code>
        to
        <code>
            activate
        </code>
        in the script above and click
        <em>
            Run
        </em>
        .
    </p>
    <p>
        Now that you’ve seen that apps can respond to scripting commands, it’s
        time to add this ability to your app.
    </p>
    <h2>
        Making Your App Scriptable
    </h2>
    <p>
        The scripting definition file of your app defines what the app can do;
        it’s a little like an API. This file lives in your app project and specifies
        several things:
    </p>
    <ul>
        <li>
            Standard scripting objects and commands, such as
            <code>
                window
            </code>
            ,
            <code>
                make
            </code>
            ,
            <code>
                delete
            </code>
            ,
            <code>
                count
            </code>
            ,
            <code>
                open
            </code>
            and
            <code>
                quit
            </code>
            .
        </li>
        <li>
            Your own scriptable objects, properties and custom commands.
        </li>
    </ul>
    <p>
        In order to make classes in your app scriptable, there are a few changes
        you’ll need to make to the app.
    </p>
    <p>
        First, the scripting interface uses Key-Value-Coding to get and set the
        properties of objects. In Objective-C, all objects conformed to the KVC
        protocol automatically, but Swift objects don’t do so unless you make them
        subclasses of
        <code>
            NSObject
        </code>
        .
    </p>
    <p>
        Next, scriptable classes need an Objective-C name that the scripting interface
        can recognize. To avoid namespace conflicts, Swift object names are mangled
        to give a unique representation. By prefixing the class definitions with
        <code>
            @objc(YourClassName)
        </code>
        , you give them a name that can be used by the scripting engine.
    </p>
    <p>
        Scriptable classes need object specifiers to help locate a particular
        object within the application or parent object, and finally, the app delegate
        must have access to the data store so it can return the application’s data
        to the scripts.
    </p>
    <p>
        You don’t necessarily have to start your own scripting definition file
        from scratch, as Apple provides a standard SDEF file that you can use.
        Look in the
        <em>
            /System/Library/ScriptingDefinitions/
        </em>
        directory for
        <em>
            CocoaStandard.sdef
        </em>
        . Open this file in Xcode and have a look; it’s XML with specific headers,
        a dictionary and inside that, the Standard Suite.
    </p>
    <p>
        This is a useful starting point, and you
        <i>
            could
        </i>
        copy and paste this XML into your own SDEF file. However, in the interest
        of clean code, it’s not a good idea to leave your SDEF file full of commands
        and objects that your app does not support. To this end, the sample project
        contains a starter SDEF file with all unnecessary entries removed.
    </p>
    <p>
        Close
        <em>
            CocoaStandard.sdef
        </em>
        and open
        <em>
            ScriptableTasks.sdef
        </em>
        . Add the following code near the end at the
        <code>
            Insert Scriptable Tasks suite here
        </code>
        comment:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1330075">
                    <td class="code" id="p133007code5">
                        <pre class="xml" style="font-family:monospace;">
                            <span style="color: #808080; font-style: italic;">
                                &lt;!-- 1 --&gt;
                            </span>
                            <span style="color: #009900;">
                                <span style="color: #000000; font-weight: bold;">
                                    &lt;suite
                                </span>
                                <span style="color: #000066;">
                                    name
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "Scriptable Tasks Suite"
                                </span>
                                <span style="color: #000066;">
                                    code
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "ScTa"
                                </span>
                                <span style="color: #000066;">
                                    description
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "Scriptable Tasks suite."
                                </span>
                                <span style="color: #000000; font-weight: bold;">
                                    &gt;
                                </span>
                            </span>
                            <span style="color: #808080; font-style: italic;">
                                &lt;!-- 2 --&gt;
                            </span>
                            <span style="color: #009900;">
                                <span style="color: #000000; font-weight: bold;">
                                    &lt;class
                                </span>
                                <span style="color: #000066;">
                                    name
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "application"
                                </span>
                                <span style="color: #000066;">
                                    code
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "capp"
                                </span>
                                <span style="color: #000066;">
                                    description
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "An application's top level scripting object."
                                </span>
                                <span style="color: #000000; font-weight: bold;">
                                    &gt;
                                </span>
                            </span>
                            <span style="color: #009900;">
                                <span style="color: #000000; font-weight: bold;">
                                    &lt;cocoa
                                </span>
                                <span style="color: #000066;">
                                    class
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "NSApplication"
                                </span>
                                <span style="color: #000000; font-weight: bold;">
                                    /&gt;
                                </span>
                            </span>
                            &nbsp;
                            <span style="color: #808080; font-style: italic;">
                                &lt;!-- 3 --&gt;
                            </span>
                            <span style="color: #009900;">
                                <span style="color: #000000; font-weight: bold;">
                                    &lt;element
                                </span>
                                <span style="color: #000066;">
                                    type
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "task"
                                </span>
                                <span style="color: #000066;">
                                    access
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "r"
                                </span>
                                <span style="color: #000000; font-weight: bold;">
                                    &gt;
                                </span>
                            </span>
                            <span style="color: #009900;">
                                <span style="color: #000000; font-weight: bold;">
                                    &lt;cocoa
                                </span>
                                <span style="color: #000066;">
                                    key
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "tasks"
                                </span>
                                <span style="color: #000000; font-weight: bold;">
                                    /&gt;
                                </span>
                            </span>
                            <span style="color: #009900;">
                                <span style="color: #000000; font-weight: bold;">
                                    &lt;/element
                                    <span style="color: #000000; font-weight: bold;">
                                        &gt;
                                    </span>
                                </span>
                            </span>
                            <span style="color: #009900;">
                                <span style="color: #000000; font-weight: bold;">
                                    &lt;/class
                                    <span style="color: #000000; font-weight: bold;">
                                        &gt;
                                    </span>
                                </span>
                            </span>
                            &nbsp;
                            <span style="color: #808080; font-style: italic;">
                                &lt;!-- Insert command here --&gt;
                            </span>
                            &nbsp;
                            <span style="color: #808080; font-style: italic;">
                                &lt;!-- 4 --&gt;
                            </span>
                            <span style="color: #009900;">
                                <span style="color: #000000; font-weight: bold;">
                                    &lt;class
                                </span>
                                <span style="color: #000066;">
                                    name
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "task"
                                </span>
                                <span style="color: #000066;">
                                    code
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "TaSk"
                                </span>
                                <span style="color: #000066;">
                                    description
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "A task item"
                                </span>
                                <span style="color: #000066;">
                                    inherits
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "item"
                                </span>
                                <span style="color: #000066;">
                                    plural
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "tasks"
                                </span>
                                <span style="color: #000000; font-weight: bold;">
                                    &gt;
                                </span>
                            </span>
                            <span style="color: #009900;">
                                <span style="color: #000000; font-weight: bold;">
                                    &lt;cocoa
                                </span>
                                <span style="color: #000066;">
                                    class
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "Task"
                                </span>
                                <span style="color: #000000; font-weight: bold;">
                                    /&gt;
                                </span>
                            </span>
                            &nbsp;
                            <span style="color: #808080; font-style: italic;">
                                &lt;!-- 5 --&gt;
                            </span>
                            <span style="color: #009900;">
                                <span style="color: #000000; font-weight: bold;">
                                    &lt;property
                                </span>
                                <span style="color: #000066;">
                                    name
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "id"
                                </span>
                                <span style="color: #000066;">
                                    code
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "ID "
                                </span>
                                <span style="color: #000066;">
                                    type
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "text"
                                </span>
                                <span style="color: #000066;">
                                    access
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "r"
                                </span>
                            </span>
                            <span style="color: #009900;">
                                <span style="color: #000066;">
                                    description
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "The unique identifier of the task."
                                </span>
                                <span style="color: #000000; font-weight: bold;">
                                    &gt;
                                </span>
                            </span>
                            <span style="color: #009900;">
                                <span style="color: #000000; font-weight: bold;">
                                    &lt;cocoa
                                </span>
                                <span style="color: #000066;">
                                    key
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "id"
                                </span>
                                <span style="color: #000000; font-weight: bold;">
                                    /&gt;
                                </span>
                            </span>
                            <span style="color: #009900;">
                                <span style="color: #000000; font-weight: bold;">
                                    &lt;/property
                                    <span style="color: #000000; font-weight: bold;">
                                        &gt;
                                    </span>
                                </span>
                            </span>
                            &nbsp;
                            <span style="color: #009900;">
                                <span style="color: #000000; font-weight: bold;">
                                    &lt;property
                                </span>
                                <span style="color: #000066;">
                                    name
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "name"
                                </span>
                                <span style="color: #000066;">
                                    code
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "pnam"
                                </span>
                                <span style="color: #000066;">
                                    type
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "text"
                                </span>
                                <span style="color: #000066;">
                                    access
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "rw"
                                </span>
                            </span>
                            <span style="color: #009900;">
                                <span style="color: #000066;">
                                    description
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "The title of the task."
                                </span>
                                <span style="color: #000000; font-weight: bold;">
                                    &gt;
                                </span>
                            </span>
                            <span style="color: #009900;">
                                <span style="color: #000000; font-weight: bold;">
                                    &lt;cocoa
                                </span>
                                <span style="color: #000066;">
                                    key
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "title"
                                </span>
                                <span style="color: #000000; font-weight: bold;">
                                    /&gt;
                                </span>
                            </span>
                            <span style="color: #009900;">
                                <span style="color: #000000; font-weight: bold;">
                                    &lt;/property
                                    <span style="color: #000000; font-weight: bold;">
                                        &gt;
                                    </span>
                                </span>
                            </span>
                            &nbsp;
                            <span style="color: #808080; font-style: italic;">
                                &lt;!-- 6 --&gt;
                            </span>
                            <span style="color: #009900;">
                                <span style="color: #000000; font-weight: bold;">
                                    &lt;property
                                </span>
                                <span style="color: #000066;">
                                    name
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "daysUntilDue"
                                </span>
                                <span style="color: #000066;">
                                    code
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "CrDa"
                                </span>
                                <span style="color: #000066;">
                                    type
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "number"
                                </span>
                                <span style="color: #000066;">
                                    access
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "rw"
                                </span>
                            </span>
                            <span style="color: #009900;">
                                <span style="color: #000066;">
                                    description
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "The number of days before this task is due."
                                </span>
                                <span style="color: #000000; font-weight: bold;">
                                    /&gt;
                                </span>
                            </span>
                            <span style="color: #009900;">
                                <span style="color: #000000; font-weight: bold;">
                                    &lt;property
                                </span>
                                <span style="color: #000066;">
                                    name
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "completed"
                                </span>
                                <span style="color: #000066;">
                                    code
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "TrFa"
                                </span>
                                <span style="color: #000066;">
                                    type
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "boolean"
                                </span>
                                <span style="color: #000066;">
                                    access
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "rw"
                                </span>
                            </span>
                            <span style="color: #009900;">
                                <span style="color: #000066;">
                                    description
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "Has the task been completed?"
                                </span>
                                <span style="color: #000000; font-weight: bold;">
                                    /&gt;
                                </span>
                            </span>
                            &nbsp;
                            <span style="color: #808080; font-style: italic;">
                                &lt;!-- 7 --&gt;
                            </span>
                            <span style="color: #808080; font-style: italic;">
                                &lt;!-- Insert element of tags here --&gt;
                            </span>
                            &nbsp;
                            <span style="color: #808080; font-style: italic;">
                                &lt;!-- Insert responds-to command here --&gt;
                            </span>
                            &nbsp;
                            <span style="color: #009900;">
                                <span style="color: #000000; font-weight: bold;">
                                    &lt;/class
                                    <span style="color: #000000; font-weight: bold;">
                                        &gt;
                                    </span>
                                </span>
                            </span>
                            &nbsp;
                            <span style="color: #808080; font-style: italic;">
                                &lt;!-- Insert tag class here --&gt;
                            </span>
                            &nbsp;
                            <span style="color: #009900;">
                                <span style="color: #000000; font-weight: bold;">
                                    &lt;/suite
                                    <span style="color: #000000; font-weight: bold;">
                                        &gt;
                                    </span>
                                </span>
                            </span>
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This chunk of XML does a lot of work. Taking it bit by bit:
    </p>
    <ol>
        <li>
            The outermost element is a
            <code>
                suite
            </code>
            , so your SDEF file now has two suites:
            <em>
                Standard Suite
            </em>
            and
            <em>
                Scriptable Tasks Suite
            </em>
            . Everything in the SDEF file needs a four-character code. Apple codes
            are nearly always in lower-case and you will use a few of them for specific
            purposes. For your own suites, classes and properties, it’s best to use
            a random mix of upper-case, lower-case and symbols to avoid conflicts.
        </li>
        <li>
            The next section defines the application and must use the code
            <code>
                "capp"
            </code>
            . You must specify the class of the application; if you had subclassed
            <code>
                NSApplication
            </code>
            , you would use your subclass name here.
        </li>
        <li>
            The application contains
            <code>
                elements
            </code>
            . In this app, the elements are stored in an array called
            <code>
                tasks
            </code>
            in the app delegate. In scripting terms, elements are the objects that
            the app or other objects can contain.
        </li>
        <li>
            The last chunk defines the
            <code>
                Task
            </code>
            class that the application contains. The plural name for accessing multiples
            is
            <code>
                tasks
            </code>
            . The class in the app that backs this object type is
            <code>
                Task
            </code>
            .
        </li>
        <li>
            The first two properties are special. Look at their codes:
            <code>
                "ID "
            </code>
            and
            <code>
                "pnam"
            </code>
            .
            <code>
                "ID "
            </code>
            (note the two spaces after the letters) identifies the unique identifier
            of the object.
            <code>
                "pnam"
            </code>
            specifies the
            <code>
                name
            </code>
            property of the object. You can access objects directly using either of
            these properties.
            <p>
                <code>
                    "ID "
                </code>
                is read-only, as scripts should not change a unique identifier, but
                <code>
                    "pnam"
                </code>
                is read-write. Both of these are text properties. The
                <code>
                    "pnam"
                </code>
                property maps to the
                <code>
                    title
                </code>
                property of the
                <code>
                    Task
                </code>
                object.
            </p>
        </li>
        <li>
            The remaining two properties are a number property for
            <code>
                daysUntilDue
            </code>
            and a Boolean for
            <code>
                completed
            </code>
            . They use the same name in the object and the script, so you don’t need
            to specify the
            <code>
                cocoa key
            </code>
            .
        </li>
        <li>
            The “Insert…” comments are placeholders for when you need to add more
            to this file.
        </li>
    </ol>
    <p>
        Open
        <em>
            Info.plist
        </em>
        , right-click in the blank space below the entries and select
        <em>
            Add Row
        </em>
        . Type an upper-case
        <em>
            S
        </em>
        and the list of suggestions will scroll to
        <em>
            Scriptable
        </em>
        . Select it and change the setting to
        <em>
            YES
        </em>
        .
    </p>
    <p>
        Repeat this process to select the next item down:
        <em>
            Scripting definition file name
        </em>
        . Set this to the name of your SDEF file:
        <em>
            ScriptableTasks.sdef
        </em>
    </p>
    <p>
        If you prefer to edit the Info.plist as source code, you can alternatively
        add the following entries inside the main dict:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1330076">
                    <td class="code" id="p133007code6">
                        <pre class="xml" style="font-family:monospace;">
                            <span style="color: #009900;">
                                <span style="color: #000000; font-weight: bold;">
                                    &lt;key
                                    <span style="color: #000000; font-weight: bold;">
                                        &gt;
                                    </span>
                                </span>
                            </span>
                            NSAppleScriptEnabled
                            <span style="color: #009900;">
                                <span style="color: #000000; font-weight: bold;">
                                    &lt;/key
                                    <span style="color: #000000; font-weight: bold;">
                                        &gt;
                                    </span>
                                </span>
                            </span>
                            <span style="color: #009900;">
                                <span style="color: #000000; font-weight: bold;">
                                    &lt;true
                                </span>
                                <span style="color: #000000; font-weight: bold;">
                                    /&gt;
                                </span>
                            </span>
                            <span style="color: #009900;">
                                <span style="color: #000000; font-weight: bold;">
                                    &lt;key
                                    <span style="color: #000000; font-weight: bold;">
                                        &gt;
                                    </span>
                                </span>
                            </span>
                            OSAScriptingDefinition
                            <span style="color: #009900;">
                                <span style="color: #000000; font-weight: bold;">
                                    &lt;/key
                                    <span style="color: #000000; font-weight: bold;">
                                        &gt;
                                    </span>
                                </span>
                            </span>
                            <span style="color: #009900;">
                                <span style="color: #000000; font-weight: bold;">
                                    &lt;string
                                    <span style="color: #000000; font-weight: bold;">
                                        &gt;
                                    </span>
                                </span>
                            </span>
                            ScriptableTasks.sdef
                            <span style="color: #009900;">
                                <span style="color: #000000; font-weight: bold;">
                                    &lt;/string
                                    <span style="color: #000000; font-weight: bold;">
                                        &gt;
                                    </span>
                                </span>
                            </span>
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Now you have to modify the app delegate to handle requests that come via
        script.
    </p>
    <p>
        Open
        <em>
            AppDelegate.swift
        </em>
        file and add the following to the end of the file:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1330077">
                    <td class="code" id="p133007code7">
                        <pre class="swift" style="font-family:monospace;">
                            extension AppDelegate { // 1 override func application(_ sender: NSApplication,
                            delegateHandlesKey key: String) -&gt; Bool { return key == "tasks" } &nbsp;
                            // 2 func insertObject(_ object: Task, inTasksAtIndex index: Int) { tasks
                            = dataProvider.insertNew(task: object, at: index) } &nbsp; func removeObjectFromTasksAtIndex(_
                            index: Int) { tasks = dataProvider.deleteTask(at: index) } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Here’s what’s going on in the code above:
    </p>
    <ol>
        <li>
            When a script asks for
            <code>
                tasks
            </code>
            data, this method will confirm that the app delegate can handle it.
        </li>
        <li>
            If a script tries to insert, edit or delete data, these methods will pass
            those requests along to
            <code>
                dataProvider
            </code>
            .
        </li>
    </ol>
    <p>
        To make the
        <code>
            Task
        </code>
        model class available to the scripts, you have to do a bit more coding.
    </p>
    <p>
        Open
        <em>
            Task.swift
        </em>
        and change the class definition line to the following:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1330078">
                    <td class="code" id="p133007code8">
                        <pre class="swift" style="font-family:monospace;">
                            @objc(Task) class Task: NSObject {
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Xcode will immediately complain that
        <code>
            init
        </code>
        requires the
        <code>
            override
        </code>
        keyword, so let Fix-It do that. This is required as this class now has
        a superclass:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1330079">
                    <td class="code" id="p133007code9">
                        <pre class="swift" style="font-family:monospace;">
                            override init() {
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        <em>
            Task.swift
        </em>
        needs one more change: an object specifier. Insert the following method
        into the
        <code>
            Task
        </code>
        class:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p13300710">
                    <td class="code" id="p133007code10">
                        <pre class="swift" style="font-family:monospace;">
                            override var objectSpecifier: NSScriptObjectSpecifier { // 1 let appDescription
                            = NSApplication.shared().classDescription as! NSScriptClassDescription
                            &nbsp; // 2 let specifier = NSUniqueIDSpecifier(containerClassDescription:
                            appDescription, containerSpecifier: nil, key: "tasks", uniqueID: id) return
                            specifier }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Taking each numbered comment in turn:
    </p>
    <ol>
        <li>
            Get a description of the app’s class since the app is the container for
            tasks.
        </li>
        <li>
            Get a description of the task by id within the app. This is why the Task
            class has an
            <code>
                id
            </code>
            property – so that each task can be correctly specified.
        </li>
    </ol>
    <p>
        You’re finally ready to start scripting your app!
    </p>
    <h2>
        Scripting Your App
    </h2>
    <p>
        Before you start, make sure to quit any running instance of the app that
        Script Editor might have opened.
    </p>
    <p>
        Build and run Scriptable Tasks; right-click on the icon in the Dock and
        select
        <em>
            Options/Show
        </em>
        in Finder. Quit the
        <em>
            Script Editor
        </em>
        app and restart it to let it pick up the changes to your app.
    </p>
    <p>
        Open the
        <em>
            Library
        </em>
        window, and drag the
        <em>
            Scriptable Tasks
        </em>
        app from the
        <em>
            Finder
        </em>
        into the
        <em>
            Library
        </em>
        window.
    </p>
    <p>
        If you get an error saying the app is not scriptable, try quitting Script
        Editor and starting it again as it sometimes doesn’t register a freshly
        built app. If it still fails to import, go back and double-check your changes
        to the SDEF file.
    </p>
    <p>
        Double-click
        <em>
            Scriptable Tasks
        </em>
        in the Library to see the app’s dictionary:
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
        You’ll see the Standard Suite and the Scriptable Tasks Suite. Click on
        the
        <em>
            Scriptable Tasks
        </em>
        suite, and you will see what you put into the SDEF file. The application
        contains tasks, and a task has four properties.
    </p>
    <p>
        Change the scripting language in the dictionary to
        <em>
            JavaScript
        </em>
        using the
        <em>
            Language
        </em>
        popup in the toolbar. You will see the same information but with one important
        change. The cases of classes and properties have changed. I have no idea
        why this is, but it’s one of those “gotchas” you need to watch out for.
    </p>
    <p>
        In
        <em>
            Script Editor
        </em>
        , make a new script file and set the editor to show
        <em>
            Log/Replies
        </em>
        . Test either of the following scripts, making sure to select the appropriate
        language in the language pop-up:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p13300711">
                    <td class="code" id="p133007code11">
                        <pre class="applescript" style="font-family:monospace;">
                            <span style="color: #ff0033; font-weight: bold;">
                                tell
                            </span>
                            <span style="color: #0066ff;">
                                application
                            </span>
                            <span style="color: #009900;">
                                "Scriptable Tasks"
                            </span>
                            <span style="color: #ff0033; font-weight: bold;">
                                get
                            </span>
                            <span style="color: #ff0033;">
                                every
                            </span>
                            task
                            <span style="color: #ff0033; font-weight: bold;">
                                end
                            </span>
                            <span style="color: #ff0033; font-weight: bold;">
                                tell
                            </span>
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        or
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p13300712">
                    <td class="code" id="p133007code12">
                        <pre class="javascript" style="font-family:monospace;">
                            app
                            <span style="color: #339933;">
                                =
                            </span>
                            Application
                            <span style="color: #009900;">
                                (
                            </span>
                            <span style="color: #3366CC;">
                                "Scriptable Tasks"
                            </span>
                            <span style="color: #009900;">
                                )
                            </span>
                            <span style="color: #339933;">
                                ;
                            </span>
                            app.
                            <span style="color: #660066;">
                                tasks
                            </span>
                            <span style="color: #009900;">
                                (
                            </span>
                            <span style="color: #009900;">
                                )
                            </span>
                            <span style="color: #339933;">
                                ;
                            </span>
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        In the log, you will see a list of the tasks by ID. For more useful information,
        edit the scripts as follows:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p13300713">
                    <td class="code" id="p133007code13">
                        <pre class="applescript" style="font-family:monospace;">
                            <span style="color: #ff0033; font-weight: bold;">
                                tell
                            </span>
                            <span style="color: #0066ff;">
                                application
                            </span>
                            <span style="color: #009900;">
                                "Scriptable Tasks"
                            </span>
                            <span style="color: #ff0033; font-weight: bold;">
                                get
                            </span>
                            <span style="color: #ff0033;">
                                the
                            </span>
                            <span style="color: #0066ff;">
                                name
                            </span>
                            <span style="color: #ff0033; font-weight: bold;">
                                of
                            </span>
                            <span style="color: #ff0033;">
                                every
                            </span>
                            task
                            <span style="color: #ff0033; font-weight: bold;">
                                end
                            </span>
                            <span style="color: #ff0033; font-weight: bold;">
                                tell
                            </span>
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        or
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p13300714">
                    <td class="code" id="p133007code14">
                        <pre class="javascript" style="font-family:monospace;">
                            app
                            <span style="color: #339933;">
                                =
                            </span>
                            Application
                            <span style="color: #009900;">
                                (
                            </span>
                            <span style="color: #3366CC;">
                                "Scriptable Tasks"
                            </span>
                            <span style="color: #009900;">
                                )
                            </span>
                            <span style="color: #339933;">
                                ;
                            </span>
                            app.
                            <span style="color: #660066;">
                                tasks
                            </span>
                            .
                            <span style="color: #000066;">
                                name
                            </span>
                            <span style="color: #009900;">
                                (
                            </span>
                            <span style="color: #009900;">
                                )
                            </span>
                            <span style="color: #339933;">
                                ;
                            </span>
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
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
        Try out a few more of the sample scripts you downloaded earlier. When
        running the scripts, make sure you set the Script Editor to show
        <em>
            Log/Replies
        </em>
        so that you can see the results along the way.
    </p>
    <p>
        Each script quits the app before running it again; this is to reset the
        data after any edits so that the sample scripts work as expected. You wouldn’t
        normally do this in your own scripts.
    </p>
    <div class="note">
        <p>
            <em>
                Note:
            </em>
            Script Editor can get very confused as you build updated versions of the
            app, because it tries to keep a version running at all times if you have
            an open script that is using the app. This often ends up as an older version
            of the app, so before every build, quit the app.
        </p>
        <p>
            If you see two copies of the Scriptable Tasks app running at any time,
            or if there appears to be a script error in any of the samples, you can
            be sure that Script Editor has glommed on to the wrong version of the app.
            The easiest fix is to quit all copies of the app and quit Script Editor.
            Clean the Xcode build (
            <em>
                Product/Clean
            </em>
            ), then build and run again.
        </p>
        <p>
            Restart Script Editor and when it opens the script, click
            <em>
                Compile
            </em>
            and then click
            <em>
                Run
            </em>
            . And if THAT doesn’t work, delete Derived Data for the app in
            <em>
                ~/Library/Developer/Xcode/DerivedData
            </em>
            .
        </p>
    </div>
    <p>
        Try out the next two sample scripts:
    </p>
    <p>
        <em>
            3. Get Tasks.scpt
        </em>
    </p>
    <p>
        This script retrieves the number of tasks and the names of tasks using
        various filters. Make note of the following:
    </p>
    <ul>
        <li>
            JavaScript counts from 0, AppleScript counts from 1.
        </li>
        <li>
            Text searches are case-insensitive.
        </li>
    </ul>
    <p>
        <em>
            4. Add Edit Tasks.scpt
        </em>
    </p>
    <p>
        This script adds new tasks, toggles the
        <code>
            completed
        </code>
        flag on the first task, and tries to create a task with the same name
        as another.
    </p>
    <p>
        Hmmm… creating a task with the same name worked! Now you have two “Feed
        the cat” tasks. The cat will be thrilled, but for the purposes of this
        app, task names should be unique. Trying to add a task with a name that
        is already in use should have produced an error.
    </p>
    <p>
        Back in
        <em>
            Xcode
        </em>
        , look in
        <em>
            AppDelegate.swift
        </em>
        and you can see that when the script wants to insert an object, the app
        delegate passes that call to its
        <code>
            dataProvider
        </code>
        . In
        <em>
            DataProvider.swift
        </em>
        , look at
        <code>
            insertNew(task:at:)
        </code>
        , which inserts an existing task into the array or appends a new task
        to the end.
    </p>
    <p>
        Time to add a check here. Replace the function with the following:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p13300715">
                    <td class="code" id="p133007code15">
                        <pre class="swift" style="font-family:monospace;">
                            mutating func insertNew(task: Task, at index: Int) -&gt; [Task] { // 1
                            if taskExists(withTitle: task.title) { // 2 let command = NSScriptCommand.current()
                            command?.scriptErrorNumber = errOSACantAssign command?.scriptErrorString
                            = "Task with the title '\(task.title)' already exists" } else { // 3 if
                            index &gt;= tasks.count { tasks.append(task) } else { tasks.insert(task,
                            at: index) } &nbsp; postNotificationOfChanges() } &nbsp; return tasks }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Here’s what each commented section does:
    </p>
    <ol>
        <li>
            Use an existing function to check if a task with this name already exists.
        </li>
        <li>
            If the name is
            <i>
                not
            </i>
            unique:
            <ul>
                <li>
                    Get a reference to the scripting command that called this function.
                </li>
                <li>
                    Set the command’s
                    <code>
                        errorNumber
                    </code>
                    and
                    <code>
                        errorString
                    </code>
                    properties;
                    <code>
                        errOSACantAssign
                    </code>
                    is one of the standard AppleScript error codes. These will be sent back
                    to the calling script.
                </li>
            </ul>
        </li>
        <li>
            If the name
            <i>
                is
            </i>
            unique:
            <ul>
                <li>
                    Process the task as before.
                </li>
                <li>
                    Post a notification of data changes. The ViewController will see this
                    and update the display.
                </li>
            </ul>
        </li>
    </ol>
    <p>
        Quit the app if running, then build and run your app. Run the
        <em>
            4. Add Edit Tasks
        </em>
        scripts again. This time you should get an error dialog and no duplicate
        tasks will be created. Sorry about that, cat…
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/04/hungry_cat.png"
        alt="Making a mac app scriptable tutorial: Hungry Cat" width="400" height="445"
        class="aligncenter size-full wp-image-133079" srcset="https://koenig-media.raywenderlich.com/uploads/2016/04/hungry_cat.png 400w, https://koenig-media.raywenderlich.com/uploads/2016/04/hungry_cat-288x320.png 288w"
        sizes="(max-width: 400px) 100vw, 400px">
    </p>
    <p>
        <em>
            5. Delete Tasks.scpt
        </em>
    </p>
    <p>
        This script deletes a task, checks if a particular task exists and deletes
        it if possible, and finally deletes all completed tasks.
    </p>
    <h2>
        Working With Nested Objects
    </h2>
    <p>
        In the sample app, the second column displays a list of tags assigned
        to each task. So far, you have no way of working with them via scripts
        – time to fix that!
    </p>
    <p>
        Object specifiers can handle a hierarchy of objects. That’s what you have
        here, with the application owning the tasks and each task owning its tags.
    </p>
    <p>
        As with the
        <code>
            Task
        </code>
        class, you need to make the
        <code>
            Tag
        </code>
        scriptable.
    </p>
    <p>
        Open
        <em>
            Tag.swift
        </em>
        and make the following changes:
    </p>
    <ul>
        <li>
            Change the class definition line to
            <code>
                @objc(Tag) class Tag: NSObject {
            </code>
        </li>
        <li>
            Add the
            <code>
                override
            </code>
            keyword to
            <code>
                init
            </code>
            .
        </li>
        <li>
            Add the object specifier method:
        </li>
    </ul>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p13300716">
                    <td class="code" id="p133007code16">
                        <pre class="swift" style="font-family:monospace;">
                            override var objectSpecifier: NSScriptObjectSpecifier { // 1 guard let
                            task = task else { return NSScriptObjectSpecifier() } &nbsp; // 2 guard
                            let taskClassDescription = task.classDescription as? NSScriptClassDescription
                            else { return NSScriptObjectSpecifier() } &nbsp; // 3 let taskSpecifier
                            = task.objectSpecifier &nbsp; // 4 let specifier = NSUniqueIDSpecifier(containerClassDescription:
                            taskClassDescription, containerSpecifier: taskSpecifier, key: "tags", uniqueID:
                            id) return specifier }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        The above code is relatively straightforward:
    </p>
    <ol>
        <li>
            Check that the tag has an assigned task.
        </li>
        <li>
            Check that the task has a class description of the correct class.
        </li>
        <li>
            Get the object specifier for the parent task.
        </li>
        <li>
            Construct the object specifier for the tag contained inside the task and
            return it.
        </li>
    </ol>
    <p>
        Add the following to the SDEF file at the
        <code>
            Insert tag class here
        </code>
        comment:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p13300717">
                    <td class="code" id="p133007code17">
                        <pre class="xml" style="font-family:monospace;">
                            <span style="color: #009900;">
                                <span style="color: #000000; font-weight: bold;">
                                    &lt;class
                                </span>
                                <span style="color: #000066;">
                                    name
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "tag"
                                </span>
                                <span style="color: #000066;">
                                    code
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "TaGg"
                                </span>
                                <span style="color: #000066;">
                                    description
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "A tag"
                                </span>
                                <span style="color: #000066;">
                                    inherits
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "item"
                                </span>
                                <span style="color: #000066;">
                                    plural
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "tags"
                                </span>
                                <span style="color: #000000; font-weight: bold;">
                                    &gt;
                                </span>
                            </span>
                            <span style="color: #009900;">
                                <span style="color: #000000; font-weight: bold;">
                                    &lt;cocoa
                                </span>
                                <span style="color: #000066;">
                                    class
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "Tag"
                                </span>
                                <span style="color: #000000; font-weight: bold;">
                                    /&gt;
                                </span>
                            </span>
                            <span style="color: #009900;">
                                <span style="color: #000000; font-weight: bold;">
                                    &lt;property
                                </span>
                                <span style="color: #000066;">
                                    name
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "id"
                                </span>
                                <span style="color: #000066;">
                                    code
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "ID "
                                </span>
                                <span style="color: #000066;">
                                    type
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "text"
                                </span>
                                <span style="color: #000066;">
                                    access
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "r"
                                </span>
                            </span>
                            <span style="color: #009900;">
                                <span style="color: #000066;">
                                    description
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "The unique identifier of the tag."
                                </span>
                                <span style="color: #000000; font-weight: bold;">
                                    &gt;
                                </span>
                            </span>
                            <span style="color: #009900;">
                                <span style="color: #000000; font-weight: bold;">
                                    &lt;cocoa
                                </span>
                                <span style="color: #000066;">
                                    key
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "uniqueID"
                                </span>
                                <span style="color: #000000; font-weight: bold;">
                                    /&gt;
                                </span>
                            </span>
                            <span style="color: #009900;">
                                <span style="color: #000000; font-weight: bold;">
                                    &lt;/property
                                    <span style="color: #000000; font-weight: bold;">
                                        &gt;
                                    </span>
                                </span>
                            </span>
                            <span style="color: #009900;">
                                <span style="color: #000000; font-weight: bold;">
                                    &lt;property
                                </span>
                                <span style="color: #000066;">
                                    name
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "name"
                                </span>
                                <span style="color: #000066;">
                                    code
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "pnam"
                                </span>
                                <span style="color: #000066;">
                                    type
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "text"
                                </span>
                                <span style="color: #000066;">
                                    access
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "rw"
                                </span>
                            </span>
                            <span style="color: #009900;">
                                <span style="color: #000066;">
                                    description
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "The name of the tag."
                                </span>
                                <span style="color: #000000; font-weight: bold;">
                                    &gt;
                                </span>
                            </span>
                            <span style="color: #009900;">
                                <span style="color: #000000; font-weight: bold;">
                                    &lt;cocoa
                                </span>
                                <span style="color: #000066;">
                                    key
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "name"
                                </span>
                                <span style="color: #000000; font-weight: bold;">
                                    /&gt;
                                </span>
                            </span>
                            <span style="color: #009900;">
                                <span style="color: #000000; font-weight: bold;">
                                    &lt;/property
                                    <span style="color: #000000; font-weight: bold;">
                                        &gt;
                                    </span>
                                </span>
                            </span>
                            <span style="color: #009900;">
                                <span style="color: #000000; font-weight: bold;">
                                    &lt;/class
                                    <span style="color: #000000; font-weight: bold;">
                                        &gt;
                                    </span>
                                </span>
                            </span>
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This is very similar to the data for the
        <code>
            Task
        </code>
        class, but a tag only has two exposed properties:
        <code>
            id
        </code>
        and
        <code>
            name
        </code>
        .
    </p>
    <p>
        Now the
        <code>
            Task
        </code>
        section has to be edited to indicate that it contains tag elements.
    </p>
    <p>
        Add the following code to the Task class XML, at the
        <code>
            Insert element of tags here
        </code>
        comment:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p13300718">
                    <td class="code" id="p133007code18">
                        <pre class="xml" style="font-family:monospace;">
                            <span style="color: #009900;">
                                <span style="color: #000000; font-weight: bold;">
                                    &lt;element
                                </span>
                                <span style="color: #000066;">
                                    type
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "tag"
                                </span>
                                <span style="color: #000066;">
                                    access
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "rw"
                                </span>
                                <span style="color: #000000; font-weight: bold;">
                                    &gt;
                                </span>
                            </span>
                            <span style="color: #009900;">
                                <span style="color: #000000; font-weight: bold;">
                                    &lt;cocoa
                                </span>
                                <span style="color: #000066;">
                                    key
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "tags"
                                </span>
                                <span style="color: #000000; font-weight: bold;">
                                    /&gt;
                                </span>
                            </span>
                            <span style="color: #009900;">
                                <span style="color: #000000; font-weight: bold;">
                                    &lt;/element
                                    <span style="color: #000000; font-weight: bold;">
                                        &gt;
                                    </span>
                                </span>
                            </span>
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Quit the app, then build and run the app again.
    </p>
    <p>
        Go back to the
        <em>
            Script Editor
        </em>
        ; if the
        <em>
            Scriptable Tasks dictionary
        </em>
        is open, close and re-open it. See if it contains information about tags.
    </p>
    <p>
        If not, remove the
        <em>
            Scriptable Tasks
        </em>
        entry from the
        <em>
            Library
        </em>
        and add it again by dragging the app into the window:
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
        Try one of the following scripts:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p13300719">
                    <td class="code" id="p133007code19">
                        <pre class="applescript" style="font-family:monospace;">
                            <span style="color: #ff0033; font-weight: bold;">
                                tell
                            </span>
                            <span style="color: #0066ff;">
                                application
                            </span>
                            <span style="color: #009900;">
                                "Scriptable Tasks"
                            </span>
                            <span style="color: #ff0033; font-weight: bold;">
                                get
                            </span>
                            <span style="color: #ff0033;">
                                the
                            </span>
                            <span style="color: #0066ff;">
                                name
                            </span>
                            <span style="color: #ff0033; font-weight: bold;">
                                of
                            </span>
                            <span style="color: #ff0033;">
                                every
                            </span>
                            tag
                            <span style="color: #ff0033; font-weight: bold;">
                                of
                            </span>
                            task
                            <span style="color: #000000;">
                                1
                            </span>
                            <span style="color: #ff0033; font-weight: bold;">
                                end
                            </span>
                            <span style="color: #ff0033; font-weight: bold;">
                                tell
                            </span>
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        or
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p13300720">
                    <td class="code" id="p133007code20">
                        <pre class="javascript" style="font-family:monospace;">
                            app
                            <span style="color: #339933;">
                                =
                            </span>
                            Application
                            <span style="color: #009900;">
                                (
                            </span>
                            <span style="color: #3366CC;">
                                "Scriptable Tasks"
                            </span>
                            <span style="color: #009900;">
                                )
                            </span>
                            <span style="color: #339933;">
                                ;
                            </span>
                            app.
                            <span style="color: #660066;">
                                tasks
                            </span>
                            <span style="color: #009900;">
                                [
                            </span>
                            <span style="color: #CC0000;">
                                0
                            </span>
                            <span style="color: #009900;">
                                ]
                            </span>
                            .
                            <span style="color: #660066;">
                                tags
                            </span>
                            .
                            <span style="color: #000066;">
                                name
                            </span>
                            <span style="color: #009900;">
                                (
                            </span>
                            <span style="color: #009900;">
                                )
                            </span>
                            <span style="color: #339933;">
                                ;
                            </span>
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        The app now lets you retrieve tags – but what about adding new ones?
    </p>
    <p>
        You may have noticed in
        <em>
            Tag.swift
        </em>
        that each
        <code>
            Tag
        </code>
        object has a weak reference to its owning task. That helps create the
        links when getting the object specifier, so this task property must be
        set when assigning a new tag to a task.
    </p>
    <p>
        Open
        <em>
            Task.swift
        </em>
        and add the following method to the
        <code>
            Task
        </code>
        class:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p13300721">
                    <td class="code" id="p133007code21">
                        <pre class="swift" style="font-family:monospace;">
                            override func newScriptingObject(of objectClass: AnyClass, forValueForKey
                            key: String, withContentsValue contentsValue: Any?, properties: [String:
                            Any]) -&gt; Any? { &nbsp; let tag: Tag = super.newScriptingObject(of: objectClass,
                            forValueForKey: key, withContentsValue: contentsValue, properties: properties)
                            as! Tag tag.task = self &nbsp; return tag }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This method is sent to the container of the new object, which why you
        put it into the
        <code>
            Task
        </code>
        class and not the
        <code>
            Tag
        </code>
        class. The call is passed to
        <code>
            super
        </code>
        to get the new tag, and then the task property is assigned.
    </p>
    <p>
        Quit and build and run your app. Now run the sample script
        <em>
            6. Tasks With Tags.scpt
        </em>
        which lists tag names, lists the tasks with a specified tag, and deletes
        and create tags.
    </p>
    <h2>
        Adding Custom Commands
    </h2>
    <p>
        There is one more step you can take when making an app scriptable: adding
        custom commands. In earlier scripts, you toggled the
        <code>
            completed
        </code>
        flag of a task directly. But wouldn’t it be better – and safer – if scripts
        didn’t change the property directly, but instead used a command to do this?
    </p>
    <p>
        Consider the following script:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p13300722">
                    <td class="code" id="p133007code22">
                        <pre class="applescript" style="font-family:monospace;">
                            mark
                            <span style="color: #ff0033;">
                                the
                            </span>
                            <span style="color: #ff0033;">
                                first
                            </span>
                            task
                            <span style="color: #ff0033;">
                                as
                            </span>
                            <span style="color: #009900;">
                                "done"
                            </span>
                            mark task
                            <span style="color: #009900;">
                                "Feed the cat"
                            </span>
                            <span style="color: #ff0033;">
                                as
                            </span>
                            <span style="color: #009900;">
                                "not done"
                            </span>
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        I’m sure you’re already reaching for the SDEF file and you would be correct:
        the command has to be defined there first.
    </p>
    <p>
        There are two steps that need to happen here:
    </p>
    <ol>
        <li>
            Tell the application that this command exists and what its parameters
            will be.
        </li>
        <li>
            Tell the Task class that it responds to the command and what method to
            call to implement it.
        </li>
    </ol>
    <p>
        Inside the Scriptable Tasks suite, but outside any class, add the following
        at the
        <em>
            Insert command here
        </em>
        comment:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p13300723">
                    <td class="code" id="p133007code23">
                        <pre class="xml" style="font-family:monospace;">
                            <span style="color: #009900;">
                                <span style="color: #000000; font-weight: bold;">
                                    &lt;command
                                </span>
                                <span style="color: #000066;">
                                    name
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "mark"
                                </span>
                                <span style="color: #000066;">
                                    code
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "TaSktext"
                                </span>
                                <span style="color: #000000; font-weight: bold;">
                                    &gt;
                                </span>
                            </span>
                            <span style="color: #009900;">
                                <span style="color: #000000; font-weight: bold;">
                                    &lt;direct-parameter
                                </span>
                                <span style="color: #000066;">
                                    description
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "One task"
                                </span>
                                <span style="color: #000066;">
                                    type
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "task"
                                </span>
                                <span style="color: #000000; font-weight: bold;">
                                    /&gt;
                                </span>
                            </span>
                            <span style="color: #009900;">
                                <span style="color: #000000; font-weight: bold;">
                                    &lt;parameter
                                </span>
                                <span style="color: #000066;">
                                    name
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "as"
                                </span>
                                <span style="color: #000066;">
                                    code
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "DFLG"
                                </span>
                                <span style="color: #000066;">
                                    description
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "'done' or 'not done'"
                                </span>
                                <span style="color: #000066;">
                                    type
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "text"
                                </span>
                                <span style="color: #000000; font-weight: bold;">
                                    &gt;
                                </span>
                            </span>
                            <span style="color: #009900;">
                                <span style="color: #000000; font-weight: bold;">
                                    &lt;cocoa
                                </span>
                                <span style="color: #000066;">
                                    key
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "doneFlag"
                                </span>
                                <span style="color: #000000; font-weight: bold;">
                                    /&gt;
                                </span>
                            </span>
                            <span style="color: #009900;">
                                <span style="color: #000000; font-weight: bold;">
                                    &lt;/parameter
                                    <span style="color: #000000; font-weight: bold;">
                                        &gt;
                                    </span>
                                </span>
                            </span>
                            <span style="color: #009900;">
                                <span style="color: #000000; font-weight: bold;">
                                    &lt;/command
                                    <span style="color: #000000; font-weight: bold;">
                                        &gt;
                                    </span>
                                </span>
                            </span>
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        “Wait a minute!” you say. “Earlier you said that codes had to be
        <i>
            four
        </i>
        characters, and now I have one with eight? What’s going on here?”
    </p>
    <p>
        When defining a method, you provide a two part code. This one combines
        the codes or types of the parameters – in this case a
        <code>
            Task
        </code>
        object with some text.
    </p>
    <p>
        Inside the
        <code>
            Task
        </code>
        class definition, at the
        <em>
            Insert responds-to command here
        </em>
        comment, add the following code:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p13300724">
                    <td class="code" id="p133007code24">
                        <pre class="xml" style="font-family:monospace;">
                            <span style="color: #009900;">
                                <span style="color: #000000; font-weight: bold;">
                                    &lt;responds-to
                                </span>
                                <span style="color: #000066;">
                                    command
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "mark"
                                </span>
                                <span style="color: #000000; font-weight: bold;">
                                    &gt;
                                </span>
                            </span>
                            <span style="color: #009900;">
                                <span style="color: #000000; font-weight: bold;">
                                    &lt;cocoa
                                </span>
                                <span style="color: #000066;">
                                    method
                                </span>
                                =
                                <span style="color: #ff0000;">
                                    "markAsDone:"
                                </span>
                                <span style="color: #000000; font-weight: bold;">
                                    /&gt;
                                </span>
                            </span>
                            <span style="color: #009900;">
                                <span style="color: #000000; font-weight: bold;">
                                    &lt;/responds-to
                                    <span style="color: #000000; font-weight: bold;">
                                        &gt;
                                    </span>
                                </span>
                            </span>
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Now head back to
        <em>
            Task.swift
        </em>
        and add the following method:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p13300725">
                    <td class="code" id="p133007code25">
                        <pre class="swift" style="font-family:monospace;">
                            func markAsDone(_ command: NSScriptCommand) { if let task = command.evaluatedReceivers
                            as? Task, let doneFlag = command.evaluatedArguments?["doneFlag"] as? String
                            { if self == task { if doneFlag == "done" { completed = true } else if
                            doneFlag == "not done" { completed = false } // if doneFlag doesn't match
                            either string, leave un-changed } } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        The parameter to
        <code>
            markAsDone(_:)
        </code>
        is an
        <code>
            NSScriptCommand
        </code>
        which has two properties of interest:
        <code>
            evaluatedReceivers
        </code>
        and
        <code>
            evaluatedArguments
        </code>
        . From them, you try to get the task and the string parameter and use
        them to adjust the task accordingly.
    </p>
    <p>
        Quit and build and run your app again. Check the dictionary in the Script
        Editor, and delete and re-import it if the
        <code>
            mark
        </code>
        command is not showing:
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
        You should now be able to run the
        <em>
            7. Custom Command.scpt
        </em>
        scripts and see your new command in operation.
    </p>
    <div class="note">
        <em>
            Note:
        </em>
        Swift 3 changed the way the commands are sent to the objects. AppleScript
        still works as expected, but the
        <code>
            mark
        </code>
        command does not work in JavaScript. I have added manual toggling of the
        <code>
            completed
        </code>
        property to the JavaScript version of
        <em>
            7. Custom Command.scpt
        </em>
        but left the original there too. Hopefully it will work after an update.
    </div>
    <h2>
        Where to Go From Here?
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
                            Want to learn even faster? Save time with our
                            <span>
                                video courses
                            </span>
                        </span>
                    </div>
                </div>
            </a>
        </div>
    </div>
    <p>
        You can download the final version of the
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/07/ScriptableTasks-Final2.zip">
            sample project here
        </a>
        .
    </p>
    <p>
        There wasn’t room to cover inter-app communication in this making a mac
        app scriptable tutorial, but to see how to work between apps, check out
        <em>
            8. Inter-App Communication.scpt
        </em>
        for some examples. This script gathers a list of incomplete tasks due
        today and tomorrow, inserts them into a new TextEdit file, styles the text
        and saves the file.
    </p>
    <p>
        For more information about scriptable apps, the official Apple docs on
        <a href="https://developer.apple.com/library/mac/documentation/AppleScript/Conceptual/AppleScriptX/Concepts/scriptable_apps.html">
            Scriptable Applications
        </a>
        are a good start, as is Apple’s
        <a href="https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/ScriptableCocoaApplications/SApps_about_apps/SAppsAboutApps.html#//apple_ref/doc/uid/TP40001976">
            Overview of Cocoa Support for Scriptable Applications
        </a>
        .
    </p>
    <p>
        Interested in learning more about JXA? Check out the
        <a href="https://developer.apple.com/library/mac/releasenotes/InterapplicationCommunication/RN-JavaScriptForAutomation/Articles/Introduction.html">
            Introduction to JavaScript for Automation Release Notes
        </a>
        .
    </p>
</div>