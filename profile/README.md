# DAFED

Just a bunch of guys from around the world with interests in technology, sharing the pain of programming; but it's mostly just memes and pictures of dogs (occasionally cats).

We sometimes write about our pain...

<!-- BLOG-POST-LIST:START -->
bulba: [Poetry, the best python packaging and dependency manager?](https://ebulba.dev/2022/09/04/poetry-the-best-python-packaging-and-demendency-manager/)
> &lt;p&gt;When we start our journey as python developers we often do not think much about our development environments, we download python, write some commands like &lt;code&gt;python -m pip install my-awesome-package&lt;/code&gt; to install package we need for that project and call it a day. This behavior while being very intuitive for beginners is inherently wrong, because at the end of the day what you do is installing bunch of random packages and messing with the system python installation, which may and probably will cause some issues. Lets examine the most common ones.&lt;/p&gt;
&lt;ul&gt;
&lt;li&gt;If your operating system uses installed python to run commands/applications in the background, by updating python or any of core packages might break that functionality.&lt;/li&gt;
&lt;li&gt;Installed python version might not be compatible with packages you might want to install &lpar;while not really a breaking issue, you are being limited to single python version&rpar;.&lt;/li&gt;
&lt;li&gt;Versions of your packages might start to collide with each other &lpar;since all of the packages require specific version of different package&rpar; preventing you from installing them, or worse, causing unexpected and untested behavior between package versions.&lt;/li&gt;
&lt;/ul&gt;
&lt;h2&gt;Virtual environments and PyEnv&lt;/h2&gt;
&lt;p&gt;There is a solution for overwriting and messing with &lt;code&gt;system&lt;/code&gt; python, called &lt;strong&gt;virtual environments&lt;/strong&gt;. To this day probably one of the most popular solutions is to use &lt;a href=&quot;https://github.com/pyenv/pyenv&quot;&gt;PyEnv&lt;/a&gt; together with &lt;a href=&quot;https://docs.python.org/3/library/venv.html&quot;&gt;venv&lt;/a&gt;. This way we can separate system python and control python versions on our device, even install any released python version, together with virtual environment for each project seems to solve above mentioned issues! &lt;span class=&quot;emoji&quot;&gt;&amp;#x1f60d;&lt;/span&gt;&lt;/p&gt;
&lt;h3&gt;Development flow with pip&lt;/h3&gt;
&lt;p&gt;Using &lt;code&gt;pyenv&lt;/code&gt; and &lt;code&gt;venv&lt;/code&gt; and managing your packages with pip is quite clunky and lets be honest feels old school enough to be my parent. You have to manually create each virtual environment, freeze your pip versions, and upload &lt;code&gt;requirements.txt&lt;/code&gt; with each project. yikes... You also lose a few handy and very clean solutions to linters management.&lt;/p&gt;
&lt;h2&gt;Poetry&lt;/h2&gt;
&lt;p&gt;&lt;a href=&quot;https://python-poetry.org/&quot;&gt;Poetry&lt;/a&gt; provides functionality of &lt;code&gt;venv&lt;/code&gt; on steroids. Lets discuss a few of them a little bit deeper. If you&#39;ve ever heard or used &lt;a href=&quot;https://getcomposer.org/&quot;&gt;Composer&lt;/a&gt; or &lt;a href=&quot;https://www.npmjs.com/&quot;&gt;npm&lt;/a&gt; Poetry takes very similar approach.&lt;/p&gt;
&lt;h3&gt;Virtual environment management&lt;/h3&gt;
&lt;p&gt;Poetry by default will create virtual environment for each of poetry project. They will be stored in one place, most likely in &lt;code&gt;~/.cache/pypoetry/virtualenvs/&lt;/code&gt; which will allow you to better setup your &lt;a href=&quot;https://code.visualstudio.com/&quot;&gt;Visual Studio Code&lt;/a&gt; since all python interpreters can be found in one folder! In addition to that, poetry will generate &lt;code&gt;poetry.lock&lt;/code&gt; file containing strict versions and hashes of your installed packages.&lt;/p&gt;
&lt;h3&gt;Additional benefits of using Poetry&lt;/h3&gt;
&lt;p&gt;Imagine being able to ignore creating &lt;code&gt;.pylintrc&lt;/code&gt;, &lt;code&gt;mypy.ini&lt;/code&gt; and similar files to manage your linters &lt;em&gt;excited face&lt;/em&gt;. Yes, &lt;code&gt;Poetry&lt;/code&gt; allows you to configure your tools inside it&#39;s &lt;code&gt;pyproject.toml&lt;/code&gt;, here is an example of that. We take care of mypy, black and pylint configurations in one place.&lt;/p&gt;
&lt;pre&gt;&lt;code class=&quot;language-python&quot;&gt;[tool.black]
line_length = 120

[tool.mypy]
plugins = [&quot;pydantic.mypy&quot;]
ignore_missing_imports = true
disallow_untyped_defs = true

[tool.pylint]
max-line-length = 120
disable = [&quot;missing-module-docstring&quot;, 
            &quot;missing-class-docstring&quot;, 
            &quot;missing-function-docstring&quot;]
&lt;/code&gt;&lt;/pre&gt;
&lt;p&gt;You can plug more tools such as &lt;code&gt;isort&lt;/code&gt; in here and everything will work in this &lt;em&gt;virtual environment&lt;/em&gt; that &lt;code&gt;Poetry&lt;/code&gt; manages.&lt;/p&gt;
&lt;p&gt;On top of that you can use &lt;a href=&quot;https://docs.renovatebot.com/modules/manager/poetry/&quot;&gt;Renovate bot&lt;/a&gt; for automatic dependency updates. This can improve your workflow in git platforms, by creating merge requests with dependency updates and lift that responsibility from developers.&lt;/p&gt;
&lt;h3&gt;How, What, Where?&lt;/h3&gt;
&lt;p&gt;To get started the best place is &lt;a href=&quot;https://python-poetry.org/docs/&quot;&gt;Poetry Documentation&lt;/a&gt;&lt;/p&gt;
&lt;p&gt;If you&#39;re lazy and do not want to read documentations, you can just install poetry, run &lt;code&gt;poetry new project-name&lt;/code&gt; then &lt;code&gt;cd&lt;/code&gt; into newly created folder and start exploring by running &lt;code&gt;poetry shell&lt;/code&gt;, &lt;code&gt;poetry add package-name&lt;/code&gt;&lt;/p&gt;
&lt;h2&gt;Conclusion&lt;/h2&gt;
&lt;p&gt;In my personal opinion, &lt;code&gt;Poetry&lt;/code&gt; is superior to plain &lt;code&gt;pip&lt;/code&gt;. At my workplace and in all my hobby projects I always use &lt;code&gt;Poetry&lt;/code&gt;. Let &lt;code&gt;pip&lt;/code&gt; and &lt;code&gt;venv&lt;/code&gt; collaboration rest together with Python2 &lpar;which was deprecated&rpar;.&lt;/p&gt;



wes4m: [Reverse engineering thermal printers](https://wes4m.io/posts/epson_rev/)
> A significant part of my current work involves dealing with thermal printers to print receipts, invoices, item slips etc ..; For those unfamiliar. I&amp;rsquo;m talking about those usually small cashier side printers that print your receipts when you buy something from a restaurant, or any other shop.
Thermal printers use a universal protocol to send/receive printing commands. This protocol is called ESC/POS. For anyone stumbling on to this post trying to figure-out what the heck is going on with those printers, I feel you.


ally: [Send WhatsApp messages in Laravel](https://ac93.uk/articles/laravel-send-whatsapp-message-with-emoji-and-variables/)
> Send a message template containing emoji from Twilio in Laravel


ally: [Consume raw SQS messages from another application with Laravel&#39;s queue](https://ac93.uk/articles/laravel-consume-raw-sqs-messages-in-its-job-queue-system/)
> Easily consume arbitrary raw AWS SQS messages by another application in your Laravel application&amp;rsquo;s queue with a Job and queue configuration.


ally: [Setting up CI to build and release multiple sets of documentation for a project](https://ac93.uk/articles/github-action-build-multiple-sets-of-documentation/)
> Learn how to set up GitHub action to build documentation &lpar;PHP, OpenAPI&rpar; from multiple generators and consolidate them all into a single gh-pages branch


ally: [Headless screenshot of a chart in Laravel with Browsershot and S3 upload](https://ac93.uk/articles/laravel-chartjs-blade-browsershot/)
> Generate and save a Chart.js chart in Laravel with Browsershot and upload it to S3

<!-- BLOG-POST-LIST:END -->

You can see more here:

* [ally](https://ac93.uk)
* bazaid
* brandon
* bulba
* soki
* [wes4m](https://wes4m.io)
