# macOS FileManager类教程：文件系统入门

#### [原文地址](https://www.raywenderlich.com/157986/filemanager-class-tutorial-macos-getting-started-file-system) 翻译：[DeveloperLx](http://weibo.com/DeveloperLx)

<div class="content-wrapper">
    <div id="attachment_124497" style="width: 260px" class="wp-caption alignright">
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/04/InteractingFileSystem-feature.png"
        alt="File Manager Case Tutorial for macOS: Getting Started with the File System"
        width="250" height="250" class="size-thumbnail wp-image-124497">
        <p class="wp-caption-text">
            macOS文件系统
        </p>
    </div>
    <p>
        在
        <em>
            macOS
        </em>
        中文件系统是每个app的基础 - 在
        <code>
            FileManager
        </code>
        类有很多来处理这个。你会在
        <em>
            Applications
        </em>
        目录下储存app，在
        <em>
            Documents
        </em>
        目录下储存文档，在
        <em>
            Library
        </em>
        目录下储存偏好和支持文件。
    </p>
    <p>
        随着文件和数据在文件系统中传播，你的app该如何查找文件和目录，使用文件和目录的路径，甚至读取及写入数据到一个文件中？
    </p>
    <p>
        那就要靠
        <code>
            FileManager
        </code>
        类了！
    </p>
    <p>
        在这个教程中，你会学到如何管理目录路径，使用URL，使用通用的文件和目录对话框，展示文件和目录信息等等！
    </p>
    <h2>
        入门
    </h2>
    <p>
        For this tutorial, you’ll start with a playground and move on to an app
        later once you’ve learned the basics.
    </p>
    <p>
        <em>
            macOS
        </em>
        uses a hierarchical file system: files &amp; folders inside folders, inside
        folders. This means that finding a particular file can be complicated.
        Each file has its own address; the structure that defines this address
        is named
        <code>
            URL
        </code>
        .
    </p>
    <p>
        Open
        <em>
            Xcode
        </em>
        and click
        <em>
            Get started with a playground
        </em>
        in the
        <em>
            Welcome to Xcode
        </em>
        window, or choose
        <em>
            File/New/Playground…
        </em>
        Set the name of the playground to
        <em>
            Files
        </em>
        , make sure the Platform is set to
        <em>
            macOS
        </em>
        and click
        <em>
            Next
        </em>
        .
    </p>
    <p>
        Select your
        <em>
            Desktop
        </em>
        and click
        <em>
            Create
        </em>
        to save the playground.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/04/NewPlayground.png"
        alt="New Playground" width="600" height="432" class="aligncenter size-full wp-image-157988"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/04/NewPlayground.png 600w, https://koenig-media.raywenderlich.com/uploads/2017/04/NewPlayground-444x320.png 444w"
        sizes="(max-width: 600px) 100vw, 600px">
    </p>
    <div class="note">
        <em>
            Note:
        </em>
        For this tutorial, the name of the playground must be
        <em>
            Files
        </em>
        and it must be located on your
        <em>
            Desktop
        </em>
        . If you gave it a different name or saved it somewhere else, please rename
        it and move it before proceeding, or else the code below just won’t work!
    </div>
    <p>
        Once the starting playground is open, delete all the lines except for
        <code>
            import Cocoa
        </code>
        .
    </p>
    <p>
        Add the following line to your playground, but don’t worry about changing
        the username for now:
    </p>
    <pre lang="swift" class="hljs javascript">
        <span class="hljs-keyword">
            let
        </span>
        completePath =
        <span class="hljs-string">
            "/Users/sarah/Desktop/Files.playground"
        </span>
    </pre>
    <p>
        <code>
            completePath
        </code>
        now contains the address, or path, of this playground file. Since
        <em>
            macOS
        </em>
        is Unix-based, this is how
        <em>
            Unix
        </em>
        (and all its variants) describe file paths. The first slash indicates
        the root directory, which in this case is your startup disk. After that,
        every slash delimits a new folder or file. So
        <em>
            Files.playground
        </em>
        is in the
        <em>
            Desktop
        </em>
        folder in the
        <em>
            sarah
        </em>
        folder in the
        <em>
            Users
        </em>
        folder on the startup drive.
    </p>
    <p>
        While this string describes the full path to this file, it isn’t the best
        way to handle addresses. Instead, you are going to convert the address
        into a
        <code>
            URL
        </code>
        by adding:
    </p>
    <pre lang="swift" class="hljs javascript">
        <span class="hljs-keyword">
            let
        </span>
        completeUrl = URL(fileURLWithPath: completePath)
    </pre>
    <p>
        In the results panel of the playground, you now see:
        <code>
            file:///Users/sarah/Desktop/Files.playground
        </code>
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/04/CreateURL.png"
        alt="Create a URL" width="700" height="103" class="aligncenter size-full wp-image-157989"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/04/CreateURL.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/04/CreateURL-480x71.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/04/CreateURL-650x96.png 650w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        “Wait a minute!” you cry. “I thought a
        <code>
            URL
        </code>
        was a web address like
        <code>
            https://www.raywenderlich.com
        </code>
        , not a directory path!”
    </p>
    <p>
        Well, yes…and yes!
    </p>
    <p>
        <code>
            URL
        </code>
        stands for
        <em>
            Uniform Resource Locator
        </em>
        — which also can point to local files and folders. Instead of
        <code>
            https://
        </code>
        , local file URLs start with
        <code>
            file://
        </code>
        . In the results panel, it looks like there are 3 slashes, but that is
        because the path itself starts with a slash.
    </p>
    <h3>
        FileManager Class
    </h3>
    <p>
        You’ve used a
        <code>
            String
        </code>
        to specify a file path and converted it to a
        <code>
            URL
        </code>
        . But while this is a valid
        <code>
            URL
        </code>
        , it won’t work — unless your user name also happens to be
        <em>
            sarah
        </em>
        . Therefore, the next step is to create a
        <code>
            URL
        </code>
        that works on anyone’s computer.
    </p>
    <p>
        To do this, you’ll use the
        <code>
            FileManager
        </code>
        class, which provides methods to handle most file-related actions in macOS.
    </p>
    <p>
        The first task is to identify your
        <em>
            Home
        </em>
        folder and replace
        <em>
            sarah
        </em>
        with your own user name.
    </p>
    <p>
        Add the following line to your playground:
    </p>
    <pre lang="swift" class="hljs cs">
        <span class="hljs-keyword">
            let
        </span>
        home = FileManager.
        <span class="hljs-keyword">
            default
        </span>
        .homeDirectoryForCurrentUser
    </pre>
    <p>
        <code>
            default
        </code>
        returns the
        <code>
            FileManager
        </code>
        class singleton instance, and
        <code>
            homeDirectoryForCurrentUser
        </code>
        contains the
        <code>
            URL
        </code>
        for the home folder of the current user.
    </p>
    <p>
        Now that you have a
        <code>
            URL
        </code>
        pointing to your home folder, you can derive the path to the playground
        by adding the following code:
    </p>
    <pre lang="swift" class="hljs javascript">
        <span class="hljs-keyword">
            let
        </span>
        playgroundPath =
        <span class="hljs-string">
            "Desktop/Files.playground"
        </span>
        <span class="hljs-keyword">
            let
        </span>
        playgroundUrl = home.appendingPathComponent(playgroundPath)
    </pre>
    <p>
        The results panel should show you the
        <code>
            URL
        </code>
        for your own home folder.
    </p>
    <p>
        Add these lines to the playground to query various
        <code>
            URL
        </code>
        properties:
    </p>
    <pre lang="swift" class="hljs">
        playgroundUrl.path playgroundUrl.absoluteString playgroundUrl.absoluteURL
        playgroundUrl.baseURL playgroundUrl.pathComponents playgroundUrl.lastPathComponent
        playgroundUrl.pathExtension playgroundUrl.isFileURL playgroundUrl.hasDirectoryPath
    </pre>
    <p>
        The
        <code>
            pathComponents
        </code>
        property is interesting, as it separates out all folder and file names
        into an array. The
        <code>
            lastPathComponent
        </code>
        and
        <code>
            pathExtension
        </code>
        properties are both quite useful in practice.
    </p>
    <p>
        Here’s what you should have in your playground:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/04/URLcomponents3.png"
        alt="URL Components" width="700" height="165" class="aligncenter size-full wp-image-158588">
    </p>
    <div class="note">
        <p>
            <em>
                Note:
            </em>
            Note that the playground file has the property
            <code>
                hasDirectoryPath
            </code>
            set to
            <coee>
                true
            </coee>
            . This marks the
            <code>
                URL
            </code>
            as representing a directory. But why is the playground file marked as
            a directory?
        </p>
        <p>
            That’s because
            <em>
                .playground
            </em>
            files are folder bundles, just like
            <em>
                .app
            </em>
            files. Right-click on the playground file and select
            <em>
                Show Package Contents
            </em>
            to see what’s inside.
        </p>
    </div>
    <p>
        The
        <code>
            URL
        </code>
        class makes it easy to edit
        <code>
            URLs
        </code>
        .
    </p>
    <p>
        Add the following code to your playground:
    </p>
    <pre lang="swift" class="hljs javascript">
        <span class="hljs-keyword">
            var
        </span>
        urlForEditing = home urlForEditing.path urlForEditing.appendPathComponent(
        <span class="hljs-string">
            "Desktop"
        </span>
        ) urlForEditing.path urlForEditing.appendPathComponent(
        <span class="hljs-string">
            "Test file"
        </span>
        ) urlForEditing.path urlForEditing.appendPathExtension(
        <span class="hljs-string">
            "txt"
        </span>
        ) urlForEditing.path urlForEditing.deletePathExtension() urlForEditing.path
        urlForEditing.deleteLastPathComponent() urlForEditing.path
    </pre>
    <p>
        Note how you show the
        <code>
            path
        </code>
        property each time so it’s easy to see what’s changed.
    </p>
    <p>
        While those commands edited the
        <code>
            URL
        </code>
        in place, you can also create a new
        <code>
            URL
        </code>
        from an existing one.
    </p>
    <p>
        To see how to do this, insert the following commands into your playground:
    </p>
    <pre lang="swift" class="hljs javascript">
        <span class="hljs-keyword">
            let
        </span>
        fileUrl = home .appendingPathComponent(
        <span class="hljs-string">
            "Desktop"
        </span>
        ) .appendingPathComponent(
        <span class="hljs-string">
            "Test file"
        </span>
        ) .appendingPathExtension(
        <span class="hljs-string">
            "txt"
        </span>
        ) fileUrl.path
        <span class="hljs-keyword">
            let
        </span>
        desktopUrl = fileUrl.deletingLastPathComponent() desktopUrl.path
    </pre>
    <p>
        These methods return new
        <code>
            URLs
        </code>
        , so chaining them into a sequence works well.
    </p>
    <p>
        The three
        <code>
            appending
        </code>
        methods could have been shortened to just one, but I’ve broken them out
        here to make the individual steps clear to you.
    </p>
    <p>
        Here’s what the playground should look like:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/04/AppendURL.png"
        alt="Append Path to a URL" width="700" height="94" class="aligncenter size-full wp-image-157992"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/04/AppendURL.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/04/AppendURL-480x64.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/04/AppendURL-650x87.png 650w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        <em>
            Checking for Files and Folders
        </em>
    </p>
    <p>
        <code>
            NSString
        </code>
        has a lot of file path manipulation methods, but Swift’s
        <code>
            String
        </code>
        struct doesn’t. Instead, you should use
        <code>
            URLs
        </code>
        when working with file paths. Working with paths in this manner will become
        even more important as Apple transitions to the new
        <em>
            Apple File System (APFS)
        </em>
        .
    </p>
    <p>
        However, there is one case where you still have to use a string representation
        of a file
        <code>
            URL
        </code>
        : checking to see if a file or folder exists. The best way to get a string
        version of a
        <code>
            URL
        </code>
        is through the
        <code>
            path
        </code>
        property.
    </p>
    <p>
        Add the following code to your playground:
    </p>
    <pre lang="swift" class="hljs cs">
        <span class="hljs-keyword">
            let
        </span>
        fileManager = FileManager.
        <span class="hljs-keyword">
            default
        </span>
        fileManager.fileExists(atPath: playgroundUrl.path)
        <span class="hljs-keyword">
            let
        </span>
        missingFile = URL(fileURLWithPath:
        <span class="hljs-string">
            "this_file_does_not_exist.missing"
        </span>
        ) fileManager.fileExists(atPath: missingFile.path)
    </pre>
    <p>
        Checking whether a folder exists is slightly more obscure, as you have
        to check if the
        <code>
            URL
        </code>
        points to a valid resource that is also a folder.
    </p>
    <p>
        This requires what I consider a very un-Swifty mechanism of using an inout
        Objective-C version of a Bool. Add the following:
    </p>
    <pre lang="swift" class="hljs javascript">
        <span class="hljs-keyword">
            var
        </span>
        isDirectory: ObjCBool =
        <span class="hljs-literal">
            false
        </span>
        fileManager.fileExists(atPath: playgroundUrl.path,
        <span class="hljs-attr">
            isDirectory
        </span>
        : &amp;isDirectory) isDirectory.boolValue
    </pre>
    <p>
        Your playground should look something like this:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/04/CheckForExistence3.png"
        alt="FileManager Class Check For File Exists" width="700" height="123"
        class="aligncenter size-full wp-image-158554" srcset="https://koenig-media.raywenderlich.com/uploads/2017/04/CheckForExistence3.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/04/CheckForExistence3-480x84.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/04/CheckForExistence3-650x114.png 650w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        A fully-annotated version of the
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/04/Files.playground-1.zip"
        sl-processed="1">
            playground
        </a>
        can be downloaded here.
    </p>
    <p>
        Now that you understand how to use
        <code>
            URL
        </code>
        to identify files and folders, close the playground. It’s time to build
        an app!
    </p>
    <h2>
        File Spy
    </h2>
    <p>
        In this part of the tutorial, you’re going to build the
        <em>
            File Spy
        </em>
        app, which lets you select a folder and view a listing of every file or
        folder inside. Selecting any item will give you more details about it.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/04/FileInfo.png"
        alt="FileManager Class File Information" width="700" height="498" class="aligncenter size-full wp-image-157994"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/04/FileInfo.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/04/FileInfo-450x320.png 450w, https://koenig-media.raywenderlich.com/uploads/2017/04/FileInfo-650x462.png 650w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        Download the
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/04/FileSpy-Starter.zip"
        sl-processed="1">
            starter app project
        </a>
        , open it in
        <em>
            Xcode
        </em>
        and click the
        <em>
            Play
        </em>
        button in the toolbar, or press
        <em>
            Command-R
        </em>
        to build and run. The UI is already set up, but you’ll need to add the
        file management bits.
    </p>
    <p>
        Your first task is to let the user select a folder and then list its contents.
        You’ll add some code behind the
        <em>
            Select Folder
        </em>
        button and use the
        <code>
            NSOpenPanel
        </code>
        class to select a folder.
    </p>
    <p>
        In
        <em>
            ViewController.swift
        </em>
        , find
        <code>
            selectFolderClicked
        </code>
        in the
        <em>
            Actions
        </em>
        section and insert the following:
    </p>
    <pre lang="swift" class="hljs swift">
        <span class="hljs-comment">
            // 1
        </span>
        <span class="hljs-keyword">
            guard
        </span>
        <span class="hljs-keyword">
            let
        </span>
        window = view.window
        <span class="hljs-keyword">
            else
        </span>
        {
        <span class="hljs-keyword">
            return
        </span>
        }
        <span class="hljs-comment">
            // 2
        </span>
        <span class="hljs-keyword">
            let
        </span>
        panel =
        <span class="hljs-type">
            NSOpenPanel
        </span>
        () panel.canChooseFiles =
        <span class="hljs-literal">
            false
        </span>
        panel.canChooseDirectories =
        <span class="hljs-literal">
            true
        </span>
        panel.allowsMultipleSelection =
        <span class="hljs-literal">
            false
        </span>
        <span class="hljs-comment">
            // 3
        </span>
        panel.beginSheetModal(
        <span class="hljs-keyword">
            for
        </span>
        : window) { (result)
        <span class="hljs-keyword">
            in
        </span>
        <span class="hljs-keyword">
            if
        </span>
        result ==
        <span class="hljs-type">
            NSFileHandlingPanelOKButton
        </span>
        {
        <span class="hljs-comment">
            // 4
        </span>
        <span class="hljs-keyword">
            self
        </span>
        .selectedFolder = panel.urls[
        <span class="hljs-number">
            0
        </span>
        ]
        <span class="hljs-built_in">
            print
        </span>
        (
        <span class="hljs-keyword">
            self
        </span>
        .selectedFolder) } }
    </pre>
    <p>
        Here’s what’s going on in the code above:
    </p>
    <ol>
        <li>
            Check that you can get a reference to the window, since that’s where the
            <code>
                NSOpenPanel
            </code>
            will be displayed.
        </li>
        <li>
            Create a new
            <code>
                NSOpenPanel
            </code>
            and set some properties to only permit a single selection which must be
            a folder.
        </li>
        <li>
            Display the
            <code>
                NSOpenPanel
            </code>
            modally in the window and use a closure to wait for the result.
        </li>
        <li>
            If the result shows that the user clicked the
            <em>
                OK
            </em>
            button (the displayed button will have a different label depending on
            your locale), get the selected
            <code>
                URL
            </code>
            and set a specific
            <code>
                ViewController
            </code>
            property. For a quick temporary test, you print the selected
            <code>
                URL
            </code>
            to the console. Ignore the warning on this line for now.
        </li>
    </ol>
    <p>
        Build and run, click the
        <em>
            Select Folder
        </em>
        button and choose a folder. Confirm that the
        <code>
            URL
        </code>
        for the selected folder prints in the console.
    </p>
    <p>
        Click the button again to open the dialog,but this time click
        <em>
            Cancel
        </em>
        . This will not print a selected
        <code>
            URL
        </code>
        .
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/04/FolderSelected.png"
        alt="Selecting a Folder" width="700" height="476" class="aligncenter size-full wp-image-157995"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/04/FolderSelected.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/04/FolderSelected-471x320.png 471w, https://koenig-media.raywenderlich.com/uploads/2017/04/FolderSelected-650x442.png 650w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        Quit the app and delete the temporary
        <code>
            print
        </code>
        statement.
    </p>
    <h3>
        Folder Contents
    </h3>
    <p>
        Now that you can select a folder, your next job is to find the contents
        of that folder and display it.
    </p>
    <p>
        The previous section of code populated a property named
        <code>
            selectedFolder
        </code>
        . Scroll to the top of the
        <code>
            ViewController
        </code>
        definition and check out the
        <code>
            selectedFolder
        </code>
        property. It’s using a
        <code>
            didSet
        </code>
        property observer to run code whenever its value is set.
    </p>
    <p>
        The key line here is the one that calls
        <code>
            contentsOf(folder:)
        </code>
        . Scroll down to the stub of this method, which is currently returning
        an empty array. Replace the entire function with the following:
    </p>
    <pre lang="swift" class="hljs swift">
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                contentsOf
            </span>
            <span class="hljs-params">
                (folder: URL)
            </span>
        </span>
        -&gt; [
        <span class="hljs-type">
            URL
        </span>
        ] {
        <span class="hljs-comment">
            // 1
        </span>
        <span class="hljs-keyword">
            let
        </span>
        fileManager =
        <span class="hljs-type">
            FileManager
        </span>
        .
        <span class="hljs-keyword">
            default
        </span>
        <span class="hljs-comment">
            // 2
        </span>
        <span class="hljs-keyword">
            do
        </span>
        {
        <span class="hljs-comment">
            // 3
        </span>
        <span class="hljs-keyword">
            let
        </span>
        contents =
        <span class="hljs-keyword">
            try
        </span>
        fileManager.contentsOfDirectory(atPath: folder.path)
        <span class="hljs-comment">
            // 4
        </span>
        <span class="hljs-keyword">
            let
        </span>
        urls = contents.
        <span class="hljs-built_in">
            map
        </span>
        {
        <span class="hljs-keyword">
            return
        </span>
        folder.appendingPathComponent($
        <span class="hljs-number">
            0
        </span>
        ) }
        <span class="hljs-keyword">
            return
        </span>
        urls }
        <span class="hljs-keyword">
            catch
        </span>
        {
        <span class="hljs-comment">
            // 5
        </span>
        <span class="hljs-keyword">
            return
        </span>
        [] } }
    </pre>
    <p>
        Stepping through what the code does:
    </p>
    <ol>
        <li>
            Get the
            <code>
                FileManager
            </code>
            class singleton, just as before.
        </li>
        <li>
            Since the
            <code>
                FileManager
            </code>
            method can throw errors, you use a
            <code>
                do...catch
            </code>
            block.
        </li>
        <li>
            Try to find the contents of the folder
            <code>
                contentsOfDirectory(atPath:)
            </code>
            and return an array of file and folder names inside.
        </li>
        <li>
            Process the returned array using
            <code>
                map
            </code>
            to convert each name into a complete
            <code>
                URL
            </code>
            with its parent folder. Then return the array.
        </li>
        <li>
            Return an empty array if
            <code>
                contentsOfDirectory(atPath:)
            </code>
            throws an error.
        </li>
    </ol>
    <p>
        The
        <code>
            selectedFolder
        </code>
        property sets the
        <code>
            filesList
        </code>
        property to the contents of the selected folder, but since you use a table
        view to show the contents, you need to define how to display each item.
    </p>
    <p>
        Scroll down to the
        <code>
            NSTableViewDataSource
        </code>
        extension. Note that
        <code>
            numberOfRows
        </code>
        already returns the number of
        <code>
            URLs
        </code>
        in the
        <code>
            filesList
        </code>
        array. Now scroll to
        <code>
            NSTableViewDelegate
        </code>
        and note that
        <code>
            tableView(_:viewFor:row:)
        </code>
        returns
        <code>
            nil
        </code>
        . You need to change that before anything will appear in the table.
    </p>
    <p>
        Replace the method with:
    </p>
    <pre lang="swift" class="hljs swift">
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                tableView
            </span>
            <span class="hljs-params">
                (
                <span class="hljs-number">
                    _
                </span>
                tableView: NSTableView, viewFor tableColumn: NSTableColumn?, row: Int)
            </span>
        </span>
        -&gt;
        <span class="hljs-type">
            NSView
        </span>
        ? {
        <span class="hljs-comment">
            // 1
        </span>
        <span class="hljs-keyword">
            let
        </span>
        item = filesList[row]
        <span class="hljs-comment">
            // 2
        </span>
        <span class="hljs-keyword">
            let
        </span>
        fileIcon =
        <span class="hljs-type">
            NSWorkspace
        </span>
        .shared().icon(forFile: item.path)
        <span class="hljs-comment">
            // 3
        </span>
        <span class="hljs-keyword">
            if
        </span>
        <span class="hljs-keyword">
            let
        </span>
        cell = tableView.make(withIdentifier:
        <span class="hljs-string">
            "FileCell"
        </span>
        , owner:
        <span class="hljs-literal">
            nil
        </span>
        )
        <span class="hljs-keyword">
            as
        </span>
        ?
        <span class="hljs-type">
            NSTableCellView
        </span>
        {
        <span class="hljs-comment">
            // 4
        </span>
        cell.textField?.stringValue = item.lastPathComponent cell.imageView?.image
        = fileIcon
        <span class="hljs-keyword">
            return
        </span>
        cell }
        <span class="hljs-comment">
            // 5
        </span>
        <span class="hljs-keyword">
            return
        </span>
        <span class="hljs-literal">
            nil
        </span>
        }
    </pre>
    <p>
        Here’s what you do in this code:
    </p>
    <ol>
        <li>
            Get the
            <code>
                URL
            </code>
            matching the row number.
        </li>
        <li>
            Get the icon for this
            <code>
                URL
            </code>
            .
            <code>
                NSWorkspace
            </code>
            is another useful singleton; this method returns the Finder icon for any
            <code>
                URL
            </code>
            .
        </li>
        <li>
            Get a reference to the cell for this table. The
            <em>
                FileCell
            </em>
            identifier was set in the
            <em>
                Storyboard
            </em>
            .
        </li>
        <li>
            If the cell exists, set its text field to show the file name and its image
            view to show the file icon.
        </li>
        <li>
            If no cell exists, return
            <code>
                nil
            </code>
            .
        </li>
    </ol>
    <p>
        Now build and run, select a folder and you should see a list of files
        and folders appear — hurray!
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/04/FolderContents.png"
        alt="Show Folder Contents" width="700" height="368" class="aligncenter size-full wp-image-157996"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/04/FolderContents.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/04/FolderContents-480x252.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/04/FolderContents-650x342.png 650w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        But clicking on a file or folder gives no useful information yet, so on
        to the next step.
    </p>
    <h3>
        Getting File Information
    </h3>
    <p>
        Open up the Finder and press
        <em>
            Command-I
        </em>
        to open a window with information about the file: creation date, modification
        date, size, permissions and so on. All that information, and more, is available
        to you through the
        <code>
            FileManager
        </code>
        class.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/04/FinderFileInfo-1.png"
        alt="File Information" width="238" height="700" class="aligncenter size-full wp-image-158016"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/04/FinderFileInfo-1.png 238w, https://koenig-media.raywenderlich.com/uploads/2017/04/FinderFileInfo-1-109x320.png 109w, https://koenig-media.raywenderlich.com/uploads/2017/04/FinderFileInfo-1-170x500.png 170w"
        sizes="(max-width: 238px) 100vw, 238px">
    </p>
    <p>
        Back in the app, still in
        <em>
            ViewController.swift
        </em>
        , look for
        <code>
            tableViewSelectionDidChange
        </code>
        . This sets the property of the
        <code>
            ViewController
        </code>
        :
        <code>
            selectedItem
        </code>
        .
    </p>
    <p>
        Scroll back to the top and look at where
        <code>
            selectedItem
        </code>
        is defined. As with
        <code>
            selectedFolder
        </code>
        , a
        <code>
            didSet
        </code>
        observer is watching for changes to this property. When the property changes,
        and if the new value is not
        <code>
            nil
        </code>
        , the observer calls
        <code>
            infoAbout(url:)
        </code>
        . This is where you will retrieve the information for display.
    </p>
    <p>
        Find
        <code>
            infoAbout
        </code>
        , which currently returns a boring static string, and replace it with
        the following:
    </p>
    <pre lang="swift" class="hljs swift">
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                infoAbout
            </span>
            <span class="hljs-params">
                (url: URL)
            </span>
        </span>
        -&gt;
        <span class="hljs-type">
            String
        </span>
        {
        <span class="hljs-comment">
            // 1
        </span>
        <span class="hljs-keyword">
            let
        </span>
        fileManager =
        <span class="hljs-type">
            FileManager
        </span>
        .
        <span class="hljs-keyword">
            default
        </span>
        <span class="hljs-comment">
            // 2
        </span>
        <span class="hljs-keyword">
            do
        </span>
        {
        <span class="hljs-comment">
            // 3
        </span>
        <span class="hljs-keyword">
            let
        </span>
        attributes =
        <span class="hljs-keyword">
            try
        </span>
        fileManager.attributesOfItem(atPath: url.path)
        <span class="hljs-keyword">
            var
        </span>
        report: [
        <span class="hljs-type">
            String
        </span>
        ] = [
        <span class="hljs-string">
            "
            <span class="hljs-subst">
                \(url.path)
            </span>
            "
        </span>
        ,
        <span class="hljs-string">
            ""
        </span>
        ]
        <span class="hljs-comment">
            // 4
        </span>
        <span class="hljs-keyword">
            for
        </span>
        (key, value)
        <span class="hljs-keyword">
            in
        </span>
        attributes {
        <span class="hljs-comment">
            // ignore NSFileExtendedAttributes as it is a messy dictionary
        </span>
        <span class="hljs-keyword">
            if
        </span>
        key.rawValue ==
        <span class="hljs-string">
            "NSFileExtendedAttributes"
        </span>
        {
        <span class="hljs-keyword">
            continue
        </span>
        } report.append(
        <span class="hljs-string">
            "
            <span class="hljs-subst">
                \(key.rawValue)
            </span>
            :\t
            <span class="hljs-subst">
                \(value)
            </span>
            "
        </span>
        ) }
        <span class="hljs-comment">
            // 5
        </span>
        <span class="hljs-keyword">
            return
        </span>
        report.joined(separator:
        <span class="hljs-string">
            "\n"
        </span>
        ) }
        <span class="hljs-keyword">
            catch
        </span>
        {
        <span class="hljs-comment">
            // 6
        </span>
        <span class="hljs-keyword">
            return
        </span>
        <span class="hljs-string">
            "No information available for
            <span class="hljs-subst">
                \(url.path)
            </span>
            "
        </span>
        } }
    </pre>
    <p>
        There are a few different things happening here, so take them one at a
        time:
    </p>
    <ol>
        <li>
            As usual, get a reference to the
            <code>
                FileManager
            </code>
            shared instance.
        </li>
        <li>
            Use
            <code>
                do...catch
            </code>
            to trap any errors.
        </li>
        <li>
            Use the
            <em>
                FileManager Class’
            </em>
            <code>
                attributesOfItem(atPath:)
            </code>
            method to try to get the file information. If this succeeds, it returns
            a dictionary of type
            <code>
                [FileAttributeKey: Any]
            </code>
            <code>
                FileAttributeKeys
            </code>
            , which are members of a struct with a String
            <code>
                rawValue
            </code>
            .
        </li>
        <li>
            Assemble the key names &amp; values into an array of tab-delimited strings.
            Ignore the
            <code>
                NSFileExtendedAttributes
            </code>
            key as it contains a messy dictionary that isn’t really useful.
        </li>
        <li>
            Join these array entries into a single string &amp; return it.
        </li>
        <li>
            If the
            <code>
                try
            </code>
            throws an error, return a default report.
        </li>
    </ol>
    <p>
        Build and run again, select a folder as before, then click on any file
        or folder in the list:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/04/FolderInfo.png"
        alt="Folder Information" width="700" height="447" class="aligncenter size-full wp-image-157998"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/04/FolderInfo.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/04/FolderInfo-480x307.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/04/FolderInfo-650x415.png 650w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        You now get a lot of useful details about the file or folder. But there’s
        still more you can do!
    </p>
    <h3>
        More Features
    </h3>
    <p>
        The app is getting better, but it’s still missing a few things:
    </p>
    <ul>
        <li>
            Clicking on
            <em>
                Show Invisible Files
            </em>
            doesn’t change anything.
        </li>
        <li>
            Double-clicking on a folder should drill into its contents.
        </li>
        <li>
            The
            <em>
                Move Up
            </em>
            button needs to move back up the folder hierarchy.
        </li>
        <li>
            <em>
                Save Info
            </em>
            should record the selected file’s details to a file.
        </li>
    </ul>
    <p>
        You’ll tackle these next.
    </p>
    <p>
        <em>
            Handling Invisible Files
        </em>
    </p>
    <p>
        In Unix systems, files and folders whose name starts with a period are
        invisible. You’ll add code to handle this case.
    </p>
    <p>
        Go to
        <code>
            contentsOf(folder:)
        </code>
        and replace the line containing
        <code>
            map
        </code>
        with the following:
    </p>
    <pre lang="swift" class="hljs bash">
        <span class="hljs-built_in">
            let
        </span>
        urls = contents .filter {
        <span class="hljs-built_in">
            return
        </span>
        showInvisibles ?
        <span class="hljs-literal">
            true
        </span>
        :
        <span class="hljs-variable">
            $0
        </span>
        .characters.first !=
        <span class="hljs-string">
            "."
        </span>
        } .map {
        <span class="hljs-built_in">
            return
        </span>
        folder.appendingPathComponent(
        <span class="hljs-variable">
            $0
        </span>
        ) }
    </pre>
    <p>
        The above adds a
        <code>
            filter
        </code>
        that rejects hidden items if the
        <code>
            showInvisibles
        </code>
        property is not
        <code>
            true
        </code>
        . Otherwise the
        <code>
            filter
        </code>
        returns every item, including hidden items.
    </p>
    <p>
        Find the
        <code>
            toggleShowInvisibles
        </code>
        method of
        <code>
            ViewController
        </code>
        and insert this into the function:
    </p>
    <pre lang="swift" class="hljs objectivec">
        <span class="hljs-comment">
            // 1
        </span>
        showInvisibles = (sender.state ==
        <span class="hljs-built_in">
            NSOnState
        </span>
        )
        <span class="hljs-comment">
            // 2
        </span>
        <span class="hljs-keyword">
            if
        </span>
        let selectedFolder = selectedFolder { filesList = contentsOf(folder: selectedFolder)
        selectedItem =
        <span class="hljs-literal">
            nil
        </span>
        tableView.reloadData() }
    </pre>
    <p>
        Here is what this code does:
    </p>
    <ol>
        <li>
            Sets the
            <code>
                showInvisibles
            </code>
            property based on the sender’s state. Since the sender is an
            <code>
                NSButton
            </code>
            , it has either
            <code>
                NSOnState
            </code>
            or
            <code>
                NSOffState
            </code>
            . Because this is a checkbox button,
            <code>
                NSOnState
            </code>
            means checked.
        </li>
        <li>
            If there is a currently
            <code>
                selectedFolder
            </code>
            , regenerate the
            <code>
                filesList
            </code>
            and update the UI.
        </li>
    </ol>
    <p>
        Build and run, select a folder and check and un-check the
        <em>
            Show Invisible Files
        </em>
        button. Depending on the folder you’re viewing, you may see files starting
        with a period when
        <em>
            Show Invisible Files
        </em>
        is checked.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/04/Invisibles.png"
        alt="Show Invisible Files" width="700" height="340" class="aligncenter size-full wp-image-157999"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/04/Invisibles.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/04/Invisibles-480x233.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/04/Invisibles-650x316.png 650w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        <em>
            Handling Double-Clicking on a Folder
        </em>
    </p>
    <p>
        In the storyboard, the table view has been assigned a
        <code>
            doubleAction
        </code>
        that calls
        <code>
            tableViewDoubleClicked
        </code>
        . Find
        <code>
            tableViewDoubleClicked
        </code>
        and replace it with the following:
    </p>
    <pre lang="swift" class="hljs swift">
        <span class="hljs-meta">
            @IBAction
        </span>
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                tableViewDoubleClicked
            </span>
            <span class="hljs-params">
                (
                <span class="hljs-number">
                    _
                </span>
                sender: Any)
            </span>
        </span>
        {
        <span class="hljs-comment">
            // 1
        </span>
        <span class="hljs-keyword">
            if
        </span>
        tableView.selectedRow &lt;
        <span class="hljs-number">
            0
        </span>
        {
        <span class="hljs-keyword">
            return
        </span>
        }
        <span class="hljs-comment">
            // 2
        </span>
        <span class="hljs-keyword">
            let
        </span>
        selectedItem = filesList[tableView.selectedRow]
        <span class="hljs-comment">
            // 3
        </span>
        <span class="hljs-keyword">
            if
        </span>
        selectedItem.hasDirectoryPath { selectedFolder = selectedItem } }
    </pre>
    <p>
        Taking the above code comment-by-comment:
    </p>
    <ol>
        <li>
            Check to see whether the double-click occurred on a populated row. Clicking
            in a blank part of the table sets the
            <code>
                tableView's
            </code>
            selectedRow to -1.
        </li>
        <li>
            Get the matching
            <code>
                URL
            </code>
            from
            <code>
                filesList
            </code>
            .
        </li>
        <li>
            If the
            <code>
                URL
            </code>
            is a folder, set the
            <code>
                ViewController's
            </code>
            <code>
                selectedFolder
            </code>
            property. Just like when you select a folder using the Select Folder button,
            setting this property triggers the property observer to read the contents
            of the folder and update the UI. If the
            <code>
                URL
            </code>
            is not a folder, nothing happens.
        </li>
    </ol>
    <p>
        Build and run, select a folder containing other folders, and then double-click
        a folder in the list to drill down into it.
    </p>
    <p>
        <em>
            Handle the Move Up Button
        </em>
    </p>
    <p>
        Once you have implemented double-click to drill down, the next obvious
        step is to move back up the tree.
    </p>
    <p>
        Find the empty
        <code>
            moveUpClicked
        </code>
        method and replace it with the following:
    </p>
    <pre lang="swift" class="hljs swift">
        <span class="hljs-meta">
            @IBAction
        </span>
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                moveUpClicked
            </span>
            <span class="hljs-params">
                (
                <span class="hljs-number">
                    _
                </span>
                sender: Any)
            </span>
        </span>
        {
        <span class="hljs-keyword">
            if
        </span>
        selectedFolder?.path ==
        <span class="hljs-string">
            "/"
        </span>
        {
        <span class="hljs-keyword">
            return
        </span>
        } selectedFolder = selectedFolder?.deletingLastPathComponent() }
    </pre>
    <p>
        This first checks to see whether the
        <code>
            selectedFolder
        </code>
        is the root folder. If so, you can’t go any higher. If not, use a
        <code>
            URL
        </code>
        method to strip the last segment off the URL. Editing
        <code>
            selectedFolder
        </code>
        will trigger the update as before.
    </p>
    <p>
        Build and run again; confirm that you can select a folder, double-click
        to move down into a sub-folder and click
        <em>
            Move Up
        </em>
        to go back up the folder hierarchy. You can move up even before double-clicking
        a folder, as long as you are not already at the root level.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/04/MoveDownUp.gif"
        alt="Move Up The Folder Tree" width="694" height="397" class="aligncenter size-full wp-image-158000">
    </p>
    <div class="note">
        <em>
            Note:
        </em>
        As you've seen, using property observers (
        <code>
            didSet
        </code>
        ) can be incredibly useful. All the code for updating the display is in
        an observer, so no matter what method or UI element changes an observed
        property, the update happens with no need to do anything else. Sweet!
    </div>
    <p>
        <em>
            Saving Information
        </em>
    </p>
    <p>
        There are two main ways to save data: user-initiated saves and automatic
        saves. For user-initiated saves, your app should prompt the user for a
        location to save the data, then write the data to that location. For automatic
        saves, the app has to figure out where to save the data.
    </p>
    <p>
        In this section, you are going to handle the case when the user clicks
        the
        <em>
            Save Info
        </em>
        button to initiate a save.
    </p>
    <p>
        You used
        <code>
            NSOpenPanel
        </code>
        to prompt the user to select a folder. This time, you are going to use
        <code>
            NSSavePanel
        </code>
        . Both
        <code>
            NSOpenPanel
        </code>
        and
        <code>
            NSSavePanel
        </code>
        are subclasses of
        <code>
            NSPanel
        </code>
        , so they have a lot in common.
    </p>
    <p>
        Replace the empty
        <code>
            saveInfoClicked
        </code>
        method with the following:
    </p>
    <pre lang="swift" class="hljs swift">
        <span class="hljs-meta">
            @IBAction
        </span>
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                saveInfoClicked
            </span>
            <span class="hljs-params">
                (
                <span class="hljs-number">
                    _
                </span>
                sender: Any)
            </span>
        </span>
        {
        <span class="hljs-comment">
            // 1
        </span>
        <span class="hljs-keyword">
            guard
        </span>
        <span class="hljs-keyword">
            let
        </span>
        window = view.window
        <span class="hljs-keyword">
            else
        </span>
        {
        <span class="hljs-keyword">
            return
        </span>
        }
        <span class="hljs-keyword">
            guard
        </span>
        <span class="hljs-keyword">
            let
        </span>
        selectedItem = selectedItem
        <span class="hljs-keyword">
            else
        </span>
        {
        <span class="hljs-keyword">
            return
        </span>
        }
        <span class="hljs-comment">
            // 2
        </span>
        <span class="hljs-keyword">
            let
        </span>
        panel =
        <span class="hljs-type">
            NSSavePanel
        </span>
        ()
        <span class="hljs-comment">
            // 3
        </span>
        panel.directoryURL =
        <span class="hljs-type">
            FileManager
        </span>
        .
        <span class="hljs-keyword">
            default
        </span>
        .homeDirectoryForCurrentUser
        <span class="hljs-comment">
            // 4
        </span>
        panel.nameFieldStringValue = selectedItem .deletingPathExtension() .appendingPathExtension(
        <span class="hljs-string">
            "fs.txt"
        </span>
        ) .lastPathComponent
        <span class="hljs-comment">
            // 5
        </span>
        panel.beginSheetModal(
        <span class="hljs-keyword">
            for
        </span>
        : window) { (result)
        <span class="hljs-keyword">
            in
        </span>
        <span class="hljs-keyword">
            if
        </span>
        result ==
        <span class="hljs-type">
            NSFileHandlingPanelOKButton
        </span>
        ,
        <span class="hljs-keyword">
            let
        </span>
        url = panel.url {
        <span class="hljs-comment">
            // 6
        </span>
        <span class="hljs-keyword">
            do
        </span>
        {
        <span class="hljs-keyword">
            let
        </span>
        infoAsText =
        <span class="hljs-keyword">
            self
        </span>
        .infoAbout(url: selectedItem)
        <span class="hljs-keyword">
            try
        </span>
        infoAsText.write(to: url, atomically:
        <span class="hljs-literal">
            true
        </span>
        , encoding: .utf8) }
        <span class="hljs-keyword">
            catch
        </span>
        {
        <span class="hljs-keyword">
            self
        </span>
        .showErrorDialogIn(window: window, title:
        <span class="hljs-string">
            "Unable to save file"
        </span>
        , message: error.localizedDescription) } } } }
    </pre>
    <p>
        Taking each numbered comment in turn:
    </p>
    <ol>
        <li>
            Confirm that everything you need is available: a window for displaying
            the panel and the
            <code>
                URL
            </code>
            whose info you are going to save.
        </li>
        <li>
            Create an
            <code>
                NSSavePanel
            </code>
            .
        </li>
        <li>
            Set the
            <code>
                directoryURL
            </code>
            property which dictates the initial folder shown in the panel.
        </li>
        <li>
            Set the
            <code>
                nameFieldStringValue
            </code>
            property to supply a default name of the file.
        </li>
        <li>
            Show the panel and wait in a closure for the user to finish.
        </li>
        <li>
            If the user selects a valid path for the data file (a valid
            <code>
                URL
            </code>
            ) and clicks the
            <em>
                OK
            </em>
            button, get the file information and write it to the selected file. If
            there is an error, show a dialog. Note that if the user clicks
            <em>
                Cancel
            </em>
            on the save dialog, you simply ignore the operation.
        </li>
    </ol>
    <p>
        <code>
            write(to:atomically:encoding)
        </code>
        is a String method that writes the string to the provided
        <code>
            URL
        </code>
        . The
        <code>
            atomically
        </code>
        option means that the string will be written to a temporary file and then
        renamed, ensuring that you won’t end up with a corrupt file — even if the
        system crashes during the write. The encoding for the text in this file
        is set to
        <em>
            UTF8
        </em>
        , which is a commonly used standard.
    </p>
    <p>
        Build and run, select a file or folder from the table and click
        <em>
            Save Info
        </em>
        . Select a save location, and click
        <em>
            Save
        </em>
        . You will end up with a text file that looks similar to the following:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/04/SavedFile.png"
        alt="File Info" width="650" height="370" class="aligncenter size-full wp-image-158001"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/04/SavedFile.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/04/SavedFile-480x273.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/04/SavedFile-266x151.png 266w"
        sizes="(max-width: 650px) 100vw, 650px">
    </p>
    <div class="note">
        <em>
            Note:
        </em>
        One neat feature of using
        <code>
            NSSavePanel
        </code>
        is that if you try to overwrite a file that already exists, your app will
        automatically display a confirmation dialog asking if you want to replace
        that file.
    </div>
    <p>
        That closes off the list of features for this app, but there is one more
        feature I think would be a nice addition: recording the selected folder
        and item so that when the app restarts, the last selected folder is re-displayed.
    </p>
    <h3>
        Saving App State
    </h3>
    <p>
        Normally, I would store app-state data in
        <code>
            UserDefaults
        </code>
        , which is saved automatically for you in the
        <em>
            Preferences
        </em>
        folder. But that doesn't allow you to do anything fancy with the file
        system. Instead, you will save this data to a dedicated app folder inside
        the
        <em>
            Application Support
        </em>
        folder.
    </p>
    <p>
        Scroll down to the end of
        <em>
            ViewController.swift
        </em>
        and you’ll see an extension dedicated to saving and restoring the user's
        selections.
    </p>
    <p>
        I’ve provided the functions that do the actual writing and reading. Writing
        uses the same
        <code>
            write(to:atomically:encoding)
        </code>
        method used when saving the info file. Reading uses a
        <code>
            String
        </code>
        initializer to create a
        <code>
            String
        </code>
        from a
        <code>
            URL
        </code>
        .
    </p>
    <p>
        The really interesting thing here is how to decide where to save the data.
        You’ll do that in
        <code>
            urlForDataStorage
        </code>
        , which is returning
        <code>
            nil
        </code>
        at the moment.
    </p>
    <p>
        Replace
        <code>
            urlForDataStorage
        </code>
        with the following:
    </p>
    <pre lang="swift" class="hljs swift">
        <span class="hljs-keyword">
            private
        </span>
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                urlForDataStorage
            </span>
            <span class="hljs-params">
                ()
            </span>
        </span>
        -&gt;
        <span class="hljs-type">
            URL
        </span>
        ? {
        <span class="hljs-comment">
            // 1
        </span>
        <span class="hljs-keyword">
            let
        </span>
        fileManager =
        <span class="hljs-type">
            FileManager
        </span>
        .
        <span class="hljs-keyword">
            default
        </span>
        <span class="hljs-comment">
            // 2
        </span>
        <span class="hljs-keyword">
            guard
        </span>
        <span class="hljs-keyword">
            let
        </span>
        folder = fileManager.urls(
        <span class="hljs-keyword">
            for
        </span>
        : .applicationSupportDirectory,
        <span class="hljs-keyword">
            in
        </span>
        : .userDomainMask).first
        <span class="hljs-keyword">
            else
        </span>
        {
        <span class="hljs-keyword">
            return
        </span>
        <span class="hljs-literal">
            nil
        </span>
        }
        <span class="hljs-comment">
            // 3
        </span>
        <span class="hljs-keyword">
            let
        </span>
        appFolder = folder.appendingPathComponent(
        <span class="hljs-string">
            "FileSpy"
        </span>
        )
        <span class="hljs-keyword">
            var
        </span>
        isDirectory:
        <span class="hljs-type">
            ObjCBool
        </span>
        =
        <span class="hljs-literal">
            false
        </span>
        <span class="hljs-keyword">
            let
        </span>
        folderExists = fileManager.fileExists(atPath: appFolder.path, isDirectory:
        &amp;isDirectory)
        <span class="hljs-keyword">
            if
        </span>
        !folderExists || !isDirectory.boolValue {
        <span class="hljs-keyword">
            do
        </span>
        {
        <span class="hljs-comment">
            // 4
        </span>
        <span class="hljs-keyword">
            try
        </span>
        fileManager.createDirectory(at: appFolder, withIntermediateDirectories:
        <span class="hljs-literal">
            true
        </span>
        , attributes:
        <span class="hljs-literal">
            nil
        </span>
        ) }
        <span class="hljs-keyword">
            catch
        </span>
        {
        <span class="hljs-keyword">
            return
        </span>
        <span class="hljs-literal">
            nil
        </span>
        } }
        <span class="hljs-comment">
            // 5
        </span>
        <span class="hljs-keyword">
            let
        </span>
        dataFileUrl = appFolder.appendingPathComponent(
        <span class="hljs-string">
            "StoredState.txt"
        </span>
        )
        <span class="hljs-keyword">
            return
        </span>
        dataFileUrl }
    </pre>
    <p>
        What is all this code doing?
    </p>
    <ol>
        <li>
            It’s your old friend
            <code>
                FileManager
            </code>
            class to the rescue again. :]
        </li>
        <li>
            The
            <code>
                FileManager
            </code>
            class has a method for returning a list of appropriate
            <code>
                URLs
            </code>
            for specific uses. In this case, you are looking for the
            <code>
                applicationSupportDirectory
            </code>
            in the current user's directory. It is unlikely to return more than one
            URL, but you only want to take the first one. You can use this method with
            different parameters to locate many different folders.
        </li>
        <li>
            As you did in the playground, append a path component to create an app-specific
            folder
            <code>
                URL
            </code>
            and check to see if it exists.
        </li>
        <li>
            If the folder does not exist, try to create it and any intermediate folders
            along the path, returning
            <code>
                nil
            </code>
            if this fails.
        </li>
        <li>
            Append another path component to create the full
            <code>
                URL
            </code>
            for the data file and return that.
        </li>
    </ol>
    <div class="note">
        <em>
            Note:
        </em>
        <code>
            .applicationSupportDirectory
        </code>
        is a short way to say
        <code>
            FileManager.SearchPathDirectory.applicationSupportDirectory
        </code>
        .
        <code>
            .userDomainMask
        </code>
        refers to
        <code>
            FileManager.SearchPathDomainMask.userDomainMask
        </code>
        . While the shorthand is much easier to type and read, it is useful to
        know where these come from, so you can find them in the documentation if
        you ever need to look them up.
    </div>
    <p>
        Build and run, select a folder, then click on a folder or file. Use the
        <em>
            Quit
        </em>
        menu item or
        <em>
            Command-Q
        </em>
        to close the app. Don’t quit via
        <em>
            Xcode
        </em>
        , or the lifecycle methods won’t trigger a save. Run the app again and
        notice it opens up to the file or folder you were viewing when you quit.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/04/FileInfo.png"
        alt="Saved App State" width="700" height="498" class="aligncenter size-full wp-image-157994"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/04/FileInfo.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/04/FileInfo-450x320.png 450w, https://koenig-media.raywenderlich.com/uploads/2017/04/FileInfo-650x462.png 650w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <div class="note">
        <em>
            Note:
        </em>
        If you want to see the stored-state data file, hold down
        <em>
            Option
        </em>
        while clicking on
        <em>
            Finder's Go
        </em>
        menu and select
        <em>
            Library
        </em>
        . In the new Finder window, open
        <em>
            Application Support
        </em>
        and look for the
        <em>
            FileSpy
        </em>
        folder. You should see the
        <em>
            StoredState.txt
        </em>
        file with your selected folder and item.
    </div>
    <h2>
        Where to Go From Here?
    </h2>
    <div class="inline-video-ad" id="sub-banner-inline">
        <div class="inline-video-ad-wrapper">
            <a href="https://videos.raywenderlich.com/courses" sl-processed="1">
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
        You can download the
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/04/FileSpy-Final.zip"
        sl-processed="1">
            final sample project
        </a>
        here.
    </p>
    <p>
        In this
        <code>
            FileManager
        </code>
        class tutorial:
    </p>
    <ol>
        <li>
            You learned how
            <code>
                URLs
            </code>
            can represent local files and folders and can show many properties available
            to you about a file or folder.
        </li>
        <li>
            You learned how you can add and remove
            <em>
                path components
            </em>
            to a
            <code>
                URL
            </code>
            .
        </li>
        <li>
            You explored the
            <code>
                FileManager
            </code>
            class which gives you access properties like
            <code>
                homeDirectoryForCurrentUser
            </code>
            , the
            <code>
                applicationSupportDirectory
            </code>
            and even
            <code>
                attributesOfItem
            </code>
            with detailed information about a file or folder.
        </li>
        <li>
            You learned how to save information to a file.
        </li>
        <li>
            You learned how to check if a file or folder exists.
        </li>
    </ol>
    <p>
        For more information, check out
        <a href="https://developer.apple.com/reference/foundation/filemanager"
        sl-processed="1">
            Apple's FileManager API Reference Documentation
        </a>
        which shows many more of the available methods in the
        <code>
            FileManager
        </code>
        class.
    </p>
    <p>
        You are now ready to begin incorporating the use of files and folders
        in your own apps.
    </p>
    <p>
        If you have any questions or comments please join the forum discussion
        below!
    </p>
</div>