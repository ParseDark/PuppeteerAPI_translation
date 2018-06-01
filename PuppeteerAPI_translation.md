##overview
Puppeteer是一个Node库，它提供了一个高级API来通过DevTools协议控制Chromium或Chrome。 Puppeteer API是分层次的，反映了浏览器结构。
+   Puppeteer:使用DevTools协议与浏览器进行通信。
+   浏览器:实例可以拥有多个浏览器上下文。
+   BrowserContext:实例定义了一个浏览会话并且可以拥有多个页面。
+   页面至少有一个框架：主框架。可能还有其他框架由iframe或框架标签创建。 框架至少有一个执行上下文 - 默认的执行上下文 - 框架的JavaScript被执行。一个框架可能有额外的与扩展关联的执行上下文。
+   Worker: 拥有一个执行上下文，并且便于与WebWorkers交互。


###环境变量
Puppeteer寻找某些环境变量来帮助其操作。如果puppeteer在环境中找不到它们，那么这些变量的小写变体将会在npm config中使用。
1.  HTTP_PROXY，HTTPS_PROXY，NO_PROXY - 定义用于下载和运行Chromium的HTTP代理设置。
2.  PUPPETEER_SKIP_CHROMIUM_DOWNLOAD - 在安装步骤中不要下载捆绑的Chromium。
3.  PUPPETEER_DOWNLOAD_HOST - 覆盖用于下载Chromium的URL的主机部分
4.  PUPPETEER_CHROMIUM_REVISION - 指定您希望在安装步骤中使用的特定版本的Chrome。

###Class:Puppeteer
Puppeteer模块提供了一种启动Chromium实例的方法。以下是使用Puppeteer驱动自动化的典型示例：
<pre><code>const puppeteer = require('puppeteer');
puppeteer.launch().then(async browser => {
  const page = await browser.newPage();
  await page.goto('https://www.google.com');
  // other actions...
  await browser.close();
});
</code></pre>

####puppeteer.connect(options)
此方法将Puppeteer添加到现有的Chromium实例。
*   options
   +   browserWSEndpoint:String 一个浏览器websocket端点连接到。
   +	ignoreHTTPSErrors:boolean 是否在导航期间忽略HTTPS错误。默认为false。
   +	slowMo:number 简体将Puppeteer操作减少指定的毫秒数。有用，这样你就可以看到发生了什么
   +	return: Promise


####puppeteer.defaultArgs()
此方法将Puppeteer添加到现有的Chromium实例。
*   returns: （返回类型：字符串数组）Chromium将与之一起启动的默认标志。

####puppeteer.executablePath()
此方法将Puppeteer添加到现有的Chromium实例。
*   returns: （返回类型：字符串）Puppeteer希望找到绑定的Chromium的路径。如果使用PUPPETEER_SKIP_CHROMIUM_DOWNLOAD跳过下载，则Chromium可能不存在（没有下载）。

####puppeteer.launch([options])——重要
该方法根据已有参数启动一个浏览器实例Chromium。当父节点node.js进程结束时，浏览器将被关闭。
*   options：在浏览器上设置的一组可配置选项。可以有以下字段：
   +   ignoreHTTPSErrors : （返回类型：布尔）是否在导航期间忽略HTTPS错误。默认为false。
   +	headless :（返回类型：布尔）是否以无头模式运行浏览器。默认为true，除非devtools选项为true。
   +	slowMo  :（返回类型：数字）将Puppeteer操作减少指定的毫秒数。有用，这样你就可以看到发生了什么。
   +	args : （返回类型：字符串数组）传递给浏览器实例的其他参数。 Chromium标志的列表可以在这里找到。
   +	ignoreDefaultArgs:（返回类型：布尔）不要使用puppeteer.defaultArgs（）。风险操作;避免使用。默认为false。
   +	handleSIGINT:（返回类型：布尔）关闭浏览器进程操作。ctrl+C.默认值为false.
   +	handleSIGTERM :（返回类型：布尔）关闭SIGTERM上的浏览器进程。默认为true。
   +	handleSIGHUP :（返回类型：布尔）关闭SIGHUP上的浏览器进程。默认为true。
   +	timeout :（返回类型：数字）等待浏览器实例启动的最长时间（以毫秒为单位）。默认为30000（30秒）。通过0禁用超时。
   +	dumpio :（返回类型：布尔）是否将浏览器进程标准输出和标准错误输入到process.stdout和process.stderr中。默认为false。
   +	userDataDir :（返回类型：String）用户数据目录地址。
   +	env :（返回类型：对象）指定浏览器可见的环境变量。缺省为process.env。
   +	devtools :（返回类型：布尔）是否为每个选项卡自动打开DevTools面板。如果该选项为true，则无头选项将设置为false。
   +	pipe :（返回类型：布尔）通过管道而不是WebSocket连接到浏览器。默认为false。
*	return:  Promise<Browser>异步浏览器实例。

