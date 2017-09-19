# OS X Stack Views：NSStackView

#### [原文地址](https://www.raywenderlich.com/122295/os-x-stack-views-nsstackview) 翻译：[DeveloperLx](http://weibo.com/DeveloperLx)

<div class="content-wrapper">
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/NS_StackView_feature.png"
        rel="attachment wp-att-127130" sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/04/NS_StackView_feature-250x250.png"
            alt="NS_StackView_feature" width="250" height="250" class="alignright size-thumbnail wp-image-127130"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/04/NS_StackView_feature-250x250.png 250w, https://koenig-media.raywenderlich.com/uploads/2016/04/NS_StackView_feature-320x320.png 320w, https://koenig-media.raywenderlich.com/uploads/2016/04/NS_StackView_feature.png 500w, https://koenig-media.raywenderlich.com/uploads/2016/04/NS_StackView_feature-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2016/04/NS_StackView_feature-64x64.png 64w, https://koenig-media.raywenderlich.com/uploads/2016/04/NS_StackView_feature-96x96.png 96w, https://koenig-media.raywenderlich.com/uploads/2016/04/NS_StackView_feature-128x128.png 128w"
            sizes="(max-width: 250px) 100vw, 250px">
        </a>
    </p>
    <p>
        We’ve all been there: that moment when you start laying down the UI of
        your app window and it all looks great.
    </p>
    <p>
        But then you have to make it practical.
    </p>
    <p>
        Once there are more than a few Cocoa controls laying around, you start
        planning how to put Auto Layout to work so that all your views reposition
        and resize as desired when the user resizes the app window.
    </p>
    <p>
        The fun starts when you add constraints in Interface Builder — things
        can get complex very quickly. Often, you’ll end up with constraints that
        contradict each other and you need to retrace your steps to find the offending
        constraint and adjust it to play nicely with the rest.
    </p>
    <p>
        Stack views were introduced with the release of OS X Mavericks, and ever
        since, they’ve spread to watchOS (well, a similar form at least) and iOS.
        The APIs for each platform differ to reflect the needs of each UI paradigm,
        but the core concept of leveraging the power of Auto Layout without the
        need to use constraints remains the same.
    </p>
    <div class="note">
        <p>
            <em>
                Note
            </em>
            : This
            <code>
                NSStackView
            </code>
            tutorial assumes basic familiarity with Auto Layout. If you’re new to
            Auto Layout go check out the
            <a href="http://www.raywenderlich.com/115440/auto-layout-tutorial-in-ios-9-part-1-getting-started-2"
            target="_blank" title="Auto Layout introduction" sl-processed="1">
                Auto Layout introduction
            </a>
            tutorial, because iOS concepts are very similar to those used for OS X.
        </p>
    </div>
    <h2>
        What is a Stack View?
    </h2>
    <p>
        A stack view allows you to arrange a number of views in a stack; it looks
        much like a table with a single column or a single row, depending whether
        you set a horizontal or vertical orientation for your stack:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/Figure1_1.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/Figure1_1-480x198.png"
            alt="Figure1_1" width="480" height="198" class="aligncenter size-medium wp-image-122299"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/Figure1_1-480x198.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/12/Figure1_1-700x289.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/12/Figure1_1.png 1248w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        At first glance, it might not look like much, but you’ll be surprised
        how much power you gain from a simple stack. You’ll also enjoy greater
        control of spacing between the arranged views, their alignment, and so
        on.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/Figure2_1.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/Figure2_1-480x231.png"
            alt="Figure2_1" width="480" height="231" class="aligncenter size-medium wp-image-122300"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/Figure2_1-480x231.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/12/Figure2_1-700x337.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/12/Figure2_1.png 1216w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        And finally, you can nest stacks. That’s where the real fun starts.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/Figure3_1.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/Figure3_1-384x320.png"
            alt="Figure3_1" width="384" height="320" class="aligncenter size-medium wp-image-122301"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/Figure3_1-384x320.png 384w, https://koenig-media.raywenderlich.com/uploads/2015/12/Figure3_1-600x500.png 600w, https://koenig-media.raywenderlich.com/uploads/2015/12/Figure3_1.png 986w"
            sizes="(max-width: 384px) 100vw, 384px">
        </a>
    </p>
    <h2>
        When to Use a Stack View in Your OS X App?
    </h2>
    <p>
        A stack view is not a silver bullet to all of your UI problems, but it
        does make many day-to-day tasks much easier. For instance, sometimes you
        can design the complete layout of a window without creating a single constraint,
        and that’s a pretty big win!
    </p>
    <p>
        Stack views are pretty handy in a number of cases, for instance when:
    </p>
    <ul>
        <li>
            You plan on using split view but don’t need the user to be able to resize
            its subviews
        </li>
        <li>
            You have a view on top or the sides of the window that shows and hides
            often, e.g. a notification bar
        </li>
        <li>
            You need to align groups of controls in any table-like layout
        </li>
        <li>
            You need a custom toolbar somewhere inside a view
        </li>
        <li>
            And so many more…
        </li>
    </ul>
    <p>
        To say there are lot of applications for a stack view would be an understatement.
        Once you finish this tutorial and try some stack view magic you’ll be able
        to spot opportunities where they can help your layout within your apps.
    </p>
    <h2>
        The Tutorial Project
    </h2>
    <p>
        In this tutorial, you’re going to work on an OS X app and implement a
        complex UI based on stack views.
    </p>
    <p>
        One of the key points you’ll learn is how to customize a stack view layout
        beyond the built-in properties. Finally, you’ll build UI animations based
        on stacks.
    </p>
    <p>
        By the time you’re finished, the app will be a fully functional raywenderlich.com
        book store and it will look like this:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/Figure4_1.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/Figure4_1-406x320.png"
            alt="Figure4_1" width="406" height="320" class="aligncenter size-medium wp-image-122302"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/Figure4_1-406x320.png 406w, https://koenig-media.raywenderlich.com/uploads/2015/12/Figure4_1-635x500.png 635w, https://koenig-media.raywenderlich.com/uploads/2015/12/Figure4_1.png 800w"
            sizes="(max-width: 406px) 100vw, 406px">
        </a>
    </p>
    <h2>
        Getting Started
    </h2>
    <p>
        In this
        <code>
            NSStackView
        </code>
        tutorial, you’ll work on an app called
        <em>
            Book Shop
        </em>
        . It’s a complete working app that allows people to browse books on the
        raywenderlich.com store and purchase them through the actual store that
        opens in their browser.
    </p>
    <p>
        Start by downloading the starter project for this tutorial:
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/BookShop-starter.zip"
        title="BookShop-starter" sl-processed="1">
            BookShop-starter
        </a>
        .
    </p>
    <p>
        Open
        <em>
            BookShop.xcodeproj
        </em>
        and select
        <em>
            Main.storyboard
        </em>
        to have a look at the current state of the app’s interface. You’ll see
        that someone had a hard time designing the UI and pretty much left you
        a big mess:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/Figure5_1.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/Figure5_1-477x320.png"
            alt="Figure5_1" width="477" height="320" class="aligncenter size-medium wp-image-122303"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/Figure5_1-477x320.png 477w, https://koenig-media.raywenderlich.com/uploads/2015/12/Figure5_1-700x470.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/12/Figure5_1.png 1400w"
            sizes="(max-width: 477px) 100vw, 477px">
        </a>
    </p>
    <p>
        No fear — thanks to stack views, finishing the app layout is as easy as
        can be!
    </p>
    <h2>
        Your First Stack View
    </h2>
    <p>
        Creating stack views in Interface Builder is really easy. In fact, you
        better pay close attention because you might blink and not notice you created
        them. :]
    </p>
    <p>
        For your first steps with stack views, you’re going to focus on the part
        of the app that shows the text data about the selected book: the title,
        the current edition and the publisher:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/Figure6_1.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/Figure6_1-480x167.png"
            alt="Figure6_1" width="480" height="167" class="aligncenter size-medium wp-image-122304"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/Figure6_1-480x167.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/12/Figure6_1-700x244.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/12/Figure6_1.png 776w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        Your first task is to align the labels
        <em>
            Title
        </em>
        and
        <em>
            iOS Animations by Tutorials
        </em>
        in a horizontal stack. This will keep those two nicely aligned.
    </p>
    <p>
        Select the
        <em>
            Title
        </em>
        label, then while pressing the
        <em>
            Command
        </em>
        key on your keyboard, select
        <em>
            iOS Animations by Tutorials
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/Figure7_1.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/Figure7_1-480x64.png"
            alt="Figure7_1" width="480" height="64" class="aligncenter size-medium wp-image-122305"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/Figure7_1-480x64.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/12/Figure7_1.png 662w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        Now find the stack button at the bottom of the Interface Builder panel
        and click it once:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/Figure8_1.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/Figure8_1.png"
            alt="Figure8_1" width="370" height="186" class="aligncenter size-full wp-image-122306">
        </a>
    </p>
    <p>
        Once you click the
        <em>
            Stack
        </em>
        button, look back at the labels: they now look like one entity, and that’s
        your first stack view!
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/Figure9_1.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/Figure9_1-480x83.png"
            alt="Figure9_1" width="480" height="83" class="aligncenter size-medium wp-image-122307"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/Figure9_1-480x83.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/12/Figure9_1.png 534w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        But what happened? You had two views selected.
    </p>
    <p>
        When you clicked on the stack button, Interface Builder checked the relative
        position between the selected views and assumed you wanted to create a
        horizontal stack! Check the Attributes Inspector that shows the stack properties:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/Figure10_1.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/Figure10_1-480x318.png"
            alt="Figure10_1" width="480" height="318" class="aligncenter size-medium wp-image-122308"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/Figure10_1-480x318.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/12/Figure10_1.png 516w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        But what if Interface Builder guessed wrong? How difficult is to have
        a vertical stack instead?
    </p>
    <p>
        It’s as simple as choosing
        <em>
            Vertical
        </em>
        from the orientation drop-down and checking the result:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/008-vertical.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/008-vertical.png"
            alt="008-vertical" width="424" height="116" class="aligncenter size-medium wp-image-122346">
        </a>
    </p>
    <p>
        That was easy! Now go back to
        <em>
            Horizontal
        </em>
        for orientation and let’s move on!
    </p>
    <p>
        Since you’re almost a pro by now, stack up the rest of the labels thusly:
    </p>
    <ul>
        <li>
            Select
            <em>
                Edition
            </em>
            and
            <em>
                1st edition
            </em>
            and click the stack button to stack them
        </li>
        <li>
            Select
            <em>
                Publisher
            </em>
            and
            <em>
                Razeware LLC
            </em>
            and click the stack button to stack those too
        </li>
    </ul>
    <p>
        Your layout should now look like this:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/009-stackviews.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/009-stackviews-480x182.png"
            alt="009-stackviews" width="480" height="182" class="aligncenter size-medium wp-image-122347"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/009-stackviews-480x182.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/12/009-stackviews.png 616w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        You now have all the labels aligned horizontally in pairs. Notice how
        you have the same spacing between sets. Each stack view applies the default
        spacing of 8 points between its views.
    </p>
    <p>
        Good going so far! Things are looking organized. :]
    </p>
    <h2>
        Nesting Stack Views
    </h2>
    <p>
        You’ve seen how easy it is to organize labels in stacks; it cost you a
        few little clicks. But wouldn’t it be great if you could somehow organize
        the three rows of text you ended up with too?
    </p>
    <p>
        Good news — this task is almost as easy! First of all, find the document
        outline button towards the lower-left corner of Interface Builder, and
        in case you don’t already have document outline pane open, click the button
        to do so.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/010-outline-button.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/010-outline-button.png"
            alt="010-outline-button" width="44" height="52" class="aligncenter size-medium wp-image-122348">
        </a>
    </p>
    <p>
        In your document outline, select the three stack views while holding the
        <em>
            Command
        </em>
        key on your keyboard, like so:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/011-selected-stacks.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/011-selected-stacks-318x320.png"
            alt="011-selected-stacks" width="318" height="320" class="aligncenter size-medium wp-image-122320"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/011-selected-stacks-318x320.png 318w, https://koenig-media.raywenderlich.com/uploads/2015/12/011-selected-stacks-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2015/12/011-selected-stacks-64x64.png 64w, https://koenig-media.raywenderlich.com/uploads/2015/12/011-selected-stacks-96x96.png 96w, https://koenig-media.raywenderlich.com/uploads/2015/12/011-selected-stacks-128x128.png 128w, https://koenig-media.raywenderlich.com/uploads/2015/12/011-selected-stacks.png 392w"
            sizes="(max-width: 318px) 100vw, 318px">
        </a>
    </p>
    <p>
        I hope you already guessed the next step. Click the
        <em>
            Stack
        </em>
        button in the bottom right to stack together those…stack views!
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/012-nested-stacks.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/012-nested-stacks-480x186.png"
            alt="012-nested-stacks" width="480" height="186" class="aligncenter size-medium wp-image-122321"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/012-nested-stacks-480x186.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/12/012-nested-stacks.png 552w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        Now you have three horizontal stack views stacked vertically! It looks
        like a little table, and that’s precisely what you wanted.
    </p>
    <p>
        Now it’s time to look into another property of stacks that you definitely
        need to use when nesting stacks. The alignment property (look it up in
        the Property Inspector while the stack view is selected) allows you to
        set how the views should be aligned in the alternate axis of the stack’s
        orientation:
    </p>
    <ul>
        <li>
            For
            <em>
                Horizontal
            </em>
            stacks,
            <em>
                Alignment
            </em>
            lets you arrange views on their top, center, bottom or base line
        </li>
        <li>
            For
            <em>
                Vertical
            </em>
            stacks,
            <em>
                Alignment
            </em>
            lets you arrange views on their leading, center and trailing
        </li>
    </ul>
    <p>
        Feel free to play with the current stack’s orientation, but ultimately,
        set it to
        <em>
            Center X
        </em>
        to center all the text rows, like so:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/013-centered-vertical.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/013-centered-vertical-480x164.png"
            alt="013-centered-vertical" width="480" height="164" class="aligncenter size-medium wp-image-122322"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/013-centered-vertical-480x164.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/12/013-centered-vertical.png 516w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        Hey that looks pretty cool! And to keep momentum up, go ahead and take
        care of that cover image too. In the document outline, select both the
        stack view (the one you just created) and the book cover image:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/014-stack-image-selected.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/014-stack-image-selected.png"
            alt="014-stack-image-selected" width="382" height="306" class="aligncenter size-full wp-image-122323">
        </a>
    </p>
    <p>
        I guess by now there’s almost no need to say it but in the spirit of being
        totally clear I will: click
        <em>
            Stack
        </em>
        to stack those two together! Set the orientation of the new stack to
        <em>
            Vertical
        </em>
        to arrange the image and the text above each other.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/015-stack-image-arranged.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/015-stack-image-arranged-333x320.png"
            alt="015-stack-image-arranged" width="333" height="320" class="aligncenter size-medium wp-image-122324"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/015-stack-image-arranged-333x320.png 333w, https://koenig-media.raywenderlich.com/uploads/2015/12/015-stack-image-arranged-521x500.png 521w, https://koenig-media.raywenderlich.com/uploads/2015/12/015-stack-image-arranged-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2015/12/015-stack-image-arranged.png 694w"
            sizes="(max-width: 333px) 100vw, 333px">
        </a>
    </p>
    <p>
        In your app, however, you want the image to appear above the texts, unlike
        the current arrangement. So, unfold the stack view in the document outline
        and drag the image view above to re-order the arranged views, like so:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/016-rearrange.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/016-rearrange.png"
            alt="016-rearrange" width="366" height="264" class="aligncenter size-full wp-image-122325">
        </a>
    </p>
    <p>
        The image view should remain a sub-view of its original parent and should
        just appear above the Stack View, which is its sibling. As soon as you
        do that the views will appear like this in Interface Builder:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/017-rearrange2.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/017-rearrange2-339x320.png"
            alt="017-rearrange2" width="339" height="320" class="aligncenter size-medium wp-image-122326"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/017-rearrange2-339x320.png 339w, https://koenig-media.raywenderlich.com/uploads/2015/12/017-rearrange2-530x500.png 530w, https://koenig-media.raywenderlich.com/uploads/2015/12/017-rearrange2.png 682w"
            sizes="(max-width: 339px) 100vw, 339px">
        </a>
    </p>
    <p>
        Now change alignment to
        <em>
            Center X
        </em>
        and spacing to
        <em>
            12
        </em>
        . This will center the image and text horizontally and add a bit of spacing
        between them.
    </p>
    <p>
        Finally, select the last stack view you created and the
        <em>
            Buy now from raywenderlich.com
        </em>
        button. Again, click the
        <em>
            Stack
        </em>
        button and make sure orientation is set to
        <em>
            Vertical
        </em>
        , alignment is
        <em>
            Center X
        </em>
        and spacing to
        <em>
            50
        </em>
        .
    </p>
    <p>
        Your final layout should look like this:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/018-final-layout.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/018-final-layout-270x320.png"
            alt="018-final-layout" width="270" height="320" class="aligncenter size-medium wp-image-122327"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/018-final-layout-270x320.png 270w, https://koenig-media.raywenderlich.com/uploads/2015/12/018-final-layout-422x500.png 422w, https://koenig-media.raywenderlich.com/uploads/2015/12/018-final-layout.png 666w"
            sizes="(max-width: 270px) 100vw, 270px">
        </a>
    </p>
    <h2>
        Customizing the Stack
    </h2>
    <p>
        So far, you’ve created a number of stack views and hopefully you’re starting
        to feel like a pro. :] You have the default stack view configuration, however,
        and in this section you’ll see how customizing the default behavior can
        provide even more flexibility at almost no cost.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/Screen-Shot-2016-01-16-at-8.22.08-PM.png"
        alt="no_cost_impossible" width="343" height="292" class="aligncenter size-full wp-image-124352">
    </p>
    <p>
        The stack views you created so far tutorial grew in size along with their
        content. In a way, you’ve only been “wrapping” views together for the sake
        of aligning them and nesting stacks.
    </p>
    <p>
        Stacks though can behave a bit differently if you fix their size and let
        them arrange their sub-views within that given space.
    </p>
    <h3>
        Full Window Layout
    </h3>
    <p>
        So far, you’ve got two “top” layout elements in your app’s UI. The former
        is the table on the left, and the latter is the stack view that wraps all
        the details about a single book plus the purchase button.
    </p>
    <p>
        No matter how you arrange those elements you ultimately want them to spread
        nicely within the app’s window.
    </p>
    <p>
        In the document outline select the table view and the top stack view you
        have so far:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/023_selected_table_stack.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/023_selected_table_stack.png"
            alt="023_selected_table_stack" width="392" height="248" class="aligncenter size-full wp-image-122332">
        </a>
    </p>
    <p>
        Next — no surprise here — click the
        <em>
            Stack
        </em>
        button at the bottom of the Interface Builder pane to stack the two selected
        views together, effectively bundling them into a new horizontal stack.
    </p>
    <p>
        Now click on the
        <em>
            Pin
        </em>
        button, which is located close to the Stack button, and enter four zeroes
        in the four boxes at the top of the popup. Make sure the four red lines
        light up while you enter the numbers in.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/024_pin_window.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/024_pin_window-480x237.png"
            alt="024_pin_window" width="480" height="237" class="aligncenter size-medium wp-image-122333"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/024_pin_window-480x237.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/12/024_pin_window.png 518w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        Finally, click
        <em>
            Add 4 Constraints
        </em>
        to pin your top stack view to the window, effectively making it a “full
        window” view.
    </p>
    <p>
        Just to make sure all views display correctly, click
        <em>
            Resolve Auto Layout
        </em>
        , located to the right of the Pin button, and choose
        <em>
            Update Frames
        </em>
        under All Views in View Controller. This will apply all current constraints
        and your layout will look like this:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/025_fill_window.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/025_fill_window-460x320.png"
            alt="025_fill_window" width="460" height="320" class="aligncenter size-medium wp-image-122334"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/025_fill_window-460x320.png 460w, https://koenig-media.raywenderlich.com/uploads/2015/12/025_fill_window-700x487.png 700w"
            sizes="(max-width: 460px) 100vw, 460px">
        </a>
    </p>
    <p>
        Since the table view has a constraint that sets its width to
        <code>
            180
        </code>
        points, the stack view respects that and lets the other arranged view
        fill all of the remaining space. Run the project and try resizing the window.
    </p>
    <p>
        The table view fills up the window vertically but it always keeps its
        width because the width is pinned with a constraint.
    </p>
    <p>
        Shift your attention to the book details. As you resize the window, the
        cover image and the texts always stay centered. Since the stack that contains
        them grows or shrinks to fill up the space not taken by the table view,
        its sub-views always stayed centered.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/037_window_fill.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/037_window_fill-480x134.png"
            alt="037_window_fill" width="480" height="134" class="aligncenter size-medium wp-image-122370"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/037_window_fill-480x134.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/12/037_window_fill.png 700w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        This is all you needed to do to make your layout fill up the window. That
        was easy, n’est–ce pas?
    </p>
    <p>
        Now look into another area of the layout where some of that same magic
        you just did could come handy.
    </p>
    <h3>
        Full Table Cell Layout
    </h3>
    <p>
        The table view doesn’t look all that nice at the moment, kind of like
        someone just threw in an image view and a label without any concern for
        alignment. Annoyingly, the text gets cut out at run time:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/026_table.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/026_table-268x320.png"
            alt="026_table" width="268" height="320" class="aligncenter size-medium wp-image-122335"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/026_table-268x320.png 268w, https://koenig-media.raywenderlich.com/uploads/2015/12/026_table-419x500.png 419w, https://koenig-media.raywenderlich.com/uploads/2015/12/026_table.png 506w"
            sizes="(max-width: 268px) 100vw, 268px">
        </a>
    </p>
    <p>
        Time for you to add some stack view goodness to that table view.
    </p>
    <p>
        In document outline, select the cell image and label. To do that, you’ll
        need to drill down through the view hierarchy as shown:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/027_selected_cell_views.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/027_selected_cell_views-372x320.png"
            alt="027_selected_cell_views" width="372" height="320" class="aligncenter size-medium wp-image-122336"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/027_selected_cell_views-372x320.png 372w, https://koenig-media.raywenderlich.com/uploads/2015/12/027_selected_cell_views-582x500.png 582w, https://koenig-media.raywenderlich.com/uploads/2015/12/027_selected_cell_views.png 642w"
            sizes="(max-width: 372px) 100vw, 372px">
        </a>
    </p>
    <p>
        Aaaand…drumroll…you guessed it: click the
        <em>
            Stack
        </em>
        button in Interface Builder. This will bundle the image and label into
        a vertical stack view.
    </p>
    <p>
        With the stack still selected, set the alignment to
        <em>
            Center X
        </em>
        . While you still have the stack selected, click on the
        <em>
            Pin
        </em>
        button at the bottom of Interface Builder and pin the stack to its parent
        view in all directions.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/028_pin_cell.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/028_pin_cell-480x265.png"
            alt="028_pin_cell" width="480" height="265" class="aligncenter size-medium wp-image-122337"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/028_pin_cell-480x265.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/12/028_pin_cell.png 500w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        Since the nearest neighbor view of the stack view is the cell view, simply
        pin the stack to the cell itself. Click
        <em>
            Add 4 Constraints
        </em>
        to finish up and close the popup.
    </p>
    <p>
        Select the stack view and click the
        <em>
            Resolve Auto Layout
        </em>
        issues button (to the right of Pin) and select
        <em>
            Update Frames
        </em>
        . The stack view takes up the whole table cell space and it now looks
        like this:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/029_final_cell.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/029_final_cell-383x320.png"
            alt="029_final_cell" width="383" height="320" class="aligncenter size-medium wp-image-122338"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/029_final_cell-383x320.png 383w, https://koenig-media.raywenderlich.com/uploads/2015/12/029_final_cell.png 448w"
            sizes="(max-width: 383px) 100vw, 383px">
        </a>
    </p>
    <p>
        Run the app and note how the stack view makes your whole table layout
        work like a charm.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/Screen-Shot-2016-02-14-at-8.01.59-PM-426x320.png"
        alt="Screen Shot 2016-02-14 at 8.01.59 PM" width="426" height="320" class="aligncenter size-medium wp-image-126599"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/Screen-Shot-2016-02-14-at-8.01.59-PM-426x320.png 426w, https://koenig-media.raywenderlich.com/uploads/2016/01/Screen-Shot-2016-02-14-at-8.01.59-PM-768x577.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/01/Screen-Shot-2016-02-14-at-8.01.59-PM-666x500.png 666w, https://koenig-media.raywenderlich.com/uploads/2016/01/Screen-Shot-2016-02-14-at-8.01.59-PM.png 800w"
        sizes="(max-width: 426px) 100vw, 426px">
    </p>
    <h2>
        Using Constraints on Arranged Views
    </h2>
    <p>
        Stack views give you the power of Auto Layout without the hassle of creating
        all the constraints yourself, but you can still design constraints manually
        if you want. And sometimes, you do want to do that; sometimes default settings
        just don’t work. :]
    </p>
    <p>
        There’s a few small issues with your layout that would benefit from a
        few constraints.
    </p>
    <p>
        Select the
        <em>
            Buy now from raywenderlich.com
        </em>
        button and click the
        <em>
            Pin
        </em>
        button at the bottom of Interface Builder. From the popup menu, click
        the checkbox next to width and enter
        <em>
            250
        </em>
        in the box.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/022_width_const.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/022_width_const-480x191.png"
            alt="022_width_const" width="480" height="191" class="aligncenter size-medium wp-image-122331"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/022_width_const-480x191.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/12/022_width_const.png 522w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        Click
        <em>
            Add 1 Constraint
        </em>
        to make it so. You’re setting the button width to
        <em>
            250
        </em>
        points, giving it nice padding on the sides so it’s easy on the eyes.
    </p>
    <p>
        Adding custom constraints is
        <i>
            that
        </i>
        easy!
    </p>
    <p>
        How about you align the window contents to the top of the window? Start
        by selecting your current top stack view.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/030_selected_top_stack.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/030_selected_top_stack-480x195.png"
            alt="030_selected_top_stack" width="480" height="195" class="aligncenter size-medium wp-image-122339"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/030_selected_top_stack-480x195.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/12/030_selected_top_stack.png 596w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        In Attributes Inspector, set alignment to
        <em>
            Top
        </em>
        . This should move the book details views up the window, like so:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/031_top_align.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/031_top_align-480x156.png"
            alt="031_top_align" width="480" height="156" class="aligncenter size-medium wp-image-122340"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/031_top_align-480x156.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/12/031_top_align-700x227.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/12/031_top_align.png 1583w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        Now you’re going to add a bit of spacing on the top so that the cover
        image is not “stuck” to the window title bar. Select the stack containing
        the book details (second down the hierarchy):
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/032_selected_second_stack.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/032_selected_second_stack-480x241.png"
            alt="032_selected_second_stack" width="480" height="241" class="aligncenter size-medium wp-image-122341"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/032_selected_second_stack-480x241.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/12/032_selected_second_stack.png 629w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        Click the
        <em>
            Pin
        </em>
        button and add a
        <em>
            Top
        </em>
        constraint with the value of
        <em>
            20
        </em>
        points:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/033_top_constraint.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/033_top_constraint-480x127.png"
            alt="033_top_constraint" width="480" height="127" class="aligncenter size-medium wp-image-122342"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/033_top_constraint-480x127.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/12/033_top_constraint.png 508w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        Click
        <em>
            Add 1 Constraint
        </em>
        , and you’ll see that the book details stack view now has 20 points as
        a top margin.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/034_small_window.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/034_small_window-370x320.png"
            alt="034_small_window" width="370" height="320" class="aligncenter size-medium wp-image-122343"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/034_small_window-370x320.png 370w, https://koenig-media.raywenderlich.com/uploads/2015/12/034_small_window-579x500.png 579w, https://koenig-media.raywenderlich.com/uploads/2015/12/034_small_window.png 1000w"
            sizes="(max-width: 370px) 100vw, 370px">
        </a>
    </p>
    <p>
        As you see, you can leave stacks to apply the default behavior and just
        add a constraint here and there to customize and perfect the layout!
    </p>
    <h2>
        Working with the Arranged Views
    </h2>
    <p>
        Now that you know how to stack up your layouts, the next level is to play
        around with the stack contents.
    </p>
    <p>
        The stack view itself is just a container and displays nothing on screen.
        It merely arranges the layout of a bunch of views, and you can access those
        via the
        <code>
            arrangedSubviews
        </code>
        property. For each arranged view, you can show and hide, animate, or remove
        it from the stack at will.
    </p>
    <h3>
        Stack View Animations
    </h3>
    <p>
        In this last section you’re going to learn the basics of working with
        arranged subviews.
    </p>
    <p>
        First of all, in order to access your stack view from code, you need to
        create an outlet for it. Open
        <em>
            ViewController.swift
        </em>
        and add a new outlet variable to the class:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1222951">
                    <td class="code" id="p122295code1">
                        <pre class="swift" style="font-family:monospace;">
                            @IBOutlet weak var topStack: NSStackView!
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Now switch back to
        <em>
            Main.storyboard
        </em>
        and drag from your
        <em>
            ViewController
        </em>
        to the top stack view in the document outline while pressing
        <em>
            Command
        </em>
        on your keyboard:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/035_connect_outlet.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/035_connect_outlet.png"
            alt="035_connect_outlet" width="388" height="248" class="aligncenter size-full wp-image-122344">
        </a>
    </p>
    <p>
        From the popup menu, select
        <em>
            topStack
        </em>
        , and voila! Your stack outlet is connected.
    </p>
    <div class="note">
        <p>
            <em>
                Note:
            </em>
            Now that you have a live outlet to the stack view you can work with it
            from code in the same manner you do for labels, button, and other Cocoa
            controls. For example you can dynamically add arranged view by calling
            the
            <code>
                addArrangedSubview(\_:)
            </code>
            method on your stack view or remove and arranged view by making use of
            <code>
                removeArrangedSubview(\_:)
            </code>
            .
        </p>
    </div>
    <p>
        Run the app and check the button in the top-right corner of the window:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/036_menu_button.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/036_menu_button.png"
            alt="036_menu_button" width="260" height="182" class="aligncenter size-full wp-image-122345">
        </a>
    </p>
    <p>
        The menu button is selected by default, but if you click it repeatedly
        you’ll see it toggles between selected and deselected states. The button
        is already connected to the method in
        <code>
            ViewController
        </code>
        called
        <code>
            actionToggleListView(\_:)
        </code>
        , so you can just add your code at the bottom of the method body.
    </p>
    <p>
        First, add an empty animation at the bottom of the method:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1222952">
                    <td class="code" id="p122295code2">
                        <pre class="swift" style="font-family:monospace;">
                            NSAnimationContext.runAnimationGroup({context in //configure the animation
                            context context.duration = 0.25 context.allowsImplicitAnimation = true
                            &nbsp; //perform the animation &nbsp; }, completionHandler: nil)
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        <code>
            runAnimationGroup()
        </code>
        allows you create UI animations by simply listing the desired changes
        in the argument closure. The animations closure gets one parameter, which
        is the animation
        <em>
            context
        </em>
        – you can adjust various aspects of the animation by changing the properties
        on the context. So far you set the animations duration and you enable implicit
        animations.
    </p>
    <div class="note">
        <p>
            <em>
                Note:
            </em>
            Unlike on iOS, in OSX there are different (but similar in effect) APIs
            to create animations. I personally like using
            <code>
                NSAnimationContext.runAnimationGroup(_)
            </code>
            because it’s the closest to what I’m using on iOS and can write my code
            easier and faster by just using the same approach on both platforms.
        </p>
    </div>
    <p>
        Next you can just toggle the visibility of the first arranged view of
        the top stack — more specifically, the table view that shows the list of
        books. To make all changes in the window layout animate nicely, also add
        a call to
        <code>
            layoutSubtreeIfNeeded()
        </code>
        .
    </p>
    <p>
        Just below the comment
        <code>
            //perform the animation
        </code>
        (but still inside the closure) insert this:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1222953">
                    <td class="code" id="p122295code3">
                        <pre class="swift" style="font-family:monospace;">
                            self.topStack.arrangedSubviews.first!.hidden = button.tag==0 ? true :
                            false self.view.layoutSubtreeIfNeeded()
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This will hide or show the book list each time you click the button. Since
        you made your changes from within an animation block, the layout flows
        nicely to accommodate your changes.
    </p>
    <div class="note">
        <p>
            <em>
                Note:
            </em>
            Just like with any other animation under Auto Layout you need to force
            a layout pass from inside the animations block to animate the changes you
            do to your views. In fact changing the
            <code>
                hidden
            </code>
            property on your first arranged view will be automatically animated, the
            rest of the arranged views however will have to change position and you’d
            like to animated those changes. That’s why at the end of the block you
            make a call to
            <code>
                layoutSubtreeIfNeeded()
            </code>
            .
        </p>
    </div>
    <p>
        And there you have the completed raywenderlich.com book store project!
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/Figure4_1.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/Figure4_1-406x320.png"
            alt="Figure4_1" width="406" height="320" class="aligncenter size-medium wp-image-122302"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/Figure4_1-406x320.png 406w, https://koenig-media.raywenderlich.com/uploads/2015/12/Figure4_1-635x500.png 635w, https://koenig-media.raywenderlich.com/uploads/2015/12/Figure4_1.png 800w"
            sizes="(max-width: 406px) 100vw, 406px">
        </a>
    </p>
    <p>
        For kicks, choose your favorite book from the list and click on the purchase
        button. This will open your default web browser and take you directly to
        the book store page:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/038_webshop.jpg"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/038_webshop-439x320.jpg"
            alt="038_webshop" width="439" height="320" class="aligncenter size-medium wp-image-122380"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/038_webshop-439x320.jpg 439w, https://koenig-media.raywenderlich.com/uploads/2015/12/038_webshop-686x500.jpg 686w, https://koenig-media.raywenderlich.com/uploads/2015/12/038_webshop.jpg 700w"
            sizes="(max-width: 439px) 100vw, 439px">
        </a>
    </p>
    <h2>
        Where to Go From Here
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
        To see the completed project, download
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/BookShop-completed-16.zip"
        rel="" sl-processed="1">
            BookShop-completed.zip
        </a>
        .
    </p>
    <p>
        This tutorial covered quite a bit! You know how to:
    </p>
    <ul>
        <li>
            Align views in your UI by bundling them in stacks
        </li>
        <li>
            Design complex layouts with nested stack views
        </li>
        <li>
            Use constraints to customize stack layouts
        </li>
        <li>
            And finally, how to interact with the arranged subviews
        </li>
    </ul>
    <p>
        If you’d like to learn more about stack views and how to use them for
        fun and profit, consider the following resources:
    </p>
    <ul>
        <li>
            Apple’s
            <a href="https://developer.apple.com/library/mac/documentation/AppKit/Reference/NSStackView_Class"
            target="_blank title=" nsstackview="" docs "=" " sl-processed="1 ">NSStackView docs</a>: Here you’ll discover more about this class’s properties and methods.</li>
            <li><a href="https://developer.apple.com/videos/play/wwdc2015-218
            " target="_blank title=" mysteries=" " of=" " auto=" " layout,=" " part=" " 1"=""
            sl-processed="1">
                Mysteries of Auto Layout, part 1
            </a>
            : In this WWDC ’15 talk you’ll learn about the motivation behind stack
            views and see some live demos.
        </li>
        <li>
            Finally, watch the
            <a href="http://www.raywenderlich.com/video-tutorials" target="_blank title="
            uistackview="" video="" series "=" " sl-processed="1
            ">UIStackView video series</a> right here because most of the concepts on iOS and OS X are the same.</li>
            <li>if you’d like to learn more about how the book list was coded in the starter project check out this great tutorial about <a href="http://www.raywenderlich.com/118835/os-x-nstableview-tutorial
            " target="_blank title=" cocoa=" " table=" " views"="" sl-processed="1">
                Cocoa table views
            </a>
        </li>
    </ul>
</div>