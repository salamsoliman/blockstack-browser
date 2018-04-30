# Blockstack Browser [![CircleCI](https://img.shields.io/circleci/project/blockstack/blockstack-browser/master.svg)](https://circleci.com/gh/blockstack/blockstack-portal/tree/master) [![License](https://img.shields.io/github/license/blockstack/blockstack-portal.svg)](https://github.com/blockstack/blockstack-portal/blob/master/LICENSE.md) [![Slack](http://chat.blockstack.org/badge.svg)](http://chat.blockstack.org/)

The Blockstack Browser Portal allows you to explore the Blockstack internet.
Blockstack浏览器（该git面向中国开发者）让人们浏览blockstack网络上的站点信息。
参与Blockstack社区请到：https://contribute.blockstack.org/ 

## Table of contents

- [最新版本下载](#最新版本下载releases)
- [开发注意项](#开发提示developing)
- [Building for macOS](#building-for-macos)
- [Building for the Web](#building-for-the-web)
- [Contributing](#contributing)
- [日志](#日志)
- [Tech Stack](#技术栈)
- [Testing](#testing)

## Releases

[下载最新版本](https://github.com/blockstack/blockstack-portal/releases)

## 开发相关提示

Blockstack（开发区块堆浏览器）需要一个安装一个本地的blockstack 内核才可以使用，首先您安装好Blockstack 内核，然后再进行开发blockstack 浏览器

### macOS开发者

Blockstack for macOS contains a Blockstack Core API endpoint & a CORS proxy.

*请注意这些配置命令仅在 macOS 10.12.4.上有效*

1. 下载并安装最新版本的mac版本blockstack浏览器 [latest release of Blockstack for Mac](https://github.com/blockstack/blockstack-portal/releases).
1. 安装blockstack
1. Option-click the Blockstack menu bar item and select "Enable Development Mode"
1. 克隆这个库: `git clone https://github.com/blockstack/blockstack-portal.git`
1. 执行这个命令: `npm install`
1. 点击Blockstack菜单选项选择"Copy Core API password"
1. 运行 `npm run dev`
1. 当调转到您的浏览器时，输入您的Core API密码然后点击保存。

### Linux

#### Part 1: Install & configure Blockstack Core

1. Install [Blockstack Core](https://github.com/blockstack/blockstack-core). Please follow the instructions in Blockstack Core's repository.
1. Setup the Blockstack Core wallet: `blockstack setup`. You will be prompted to select a wallet password. *Skip this step if you already have a Core wallet*
1. Start the Blockstack Core API: `blockstack api start --api_password <core-api-password> --password <wallet-password>` where `<core-api-password>` is a String value you select and `<wallet-password>` is the wallet password you selected previously.
1. Make sure there's a local Blockstack Core API running by checking `http://localhost:6270/v1/names/blockstack.id` to see if it returns a response.

#### Part 2: Install Blockstack Portal

1. Clone this repo: `git clone https://github.com/blockstack/blockstack-portal.git`
1. Install node dependencies: `npm install`
1. Run `npm run dev-proxy` to start the CORS proxy
1. Run `npm run dev`
1. When prompted in your browser, enter the Core API password you selected in part 1.


*Note: npm dev runs a BrowserSync process that watches the assets in `/app`, then builds them and places them in `/build`, and in turn serves them up on port 3000. When changes are made to the original files, they are rebuilt and re-synced to the browser frames you have open.*


## Building for macOS

1. Make sure you have a working installation of Xcode 8 or higher & valid Mac Developer signing certificate
1. Make sure you have an OpenSSL ready for bottling by homebrew by running `brew install openssl --build-bottle`
1. Make sure you have `hg` installed by running `brew install hg`
1. Run `npm install nexe -g` to install the "node to native" binary tool globally
1. Open the Blockstack macOS project in Xcode and configure your code signing development team (You only need to do this once)
1. Run `npm run mac` to build a debug release signed with your Mac Developer certificate

*Note: You only need to run `nexe` once but the first build will take a while as `nexe` downloads and compiles a source copy of node. Then it creates and copies the needed proxy binaries into place and copies a built version of the browser web app into the source tree.*

*Note: This has only been tested on macOS Sierra 10.12.4*

### Building a macOS release for distribution

1. Ensure you have valid Developer ID signing credentials in your Keychain. (See https://developer.apple.com/developer-id/ for more information)
1. Follow the instructions in the above section for building for macOS.
1. Open the Blockstack macOS project in Xcode.
1. Select the Product menu and click Archive.
1. When the archive build completes, the Organizer window will open. Select your new build.
1. Click "Export..."
1. Click "Export a Developer ID-signed Application"
1. Choose the development team with the Developer ID you'd like to use to sign the application.
1. Click "Export" and select the location to which you would like to save the signed build.


## Building for the Web

1. Make sure you've cloned the repo and installed all npm assets (as shown above)
1. Run `npm run web`


## 如何为这个社区做贡献

我们期待全世界的开发者参与到这个开源工程中来，
如果你热爱这个工程请到 [contributing guidelines](/CONTRIBUTING.md). https://contribute.blockstack.org/ ，在这个里面，您可以看到很多待处理的问题、编码标准、开发相关的笔记记录。
## Logging日志部分

这个浏览器使用`log4js`作为日志，macOS 应用使用`os_log` 作为日志。

### macOS

On macOS, the Portal sends log events to the macOS
app's log server. These are then included in macOS's unified logging API. You
can view logs by starting `Console.app`. Set up a filter the `Blockstack` process
to only see Blockstack logs. If you'd like to see more detail, in enable inclusion
of Info and Debug messages in the Action menu.

#### Sending logs to developers

Blockstack logs are included in macOS's unified logging system. This allows
us to easily collect a large amount of information about the user's system when
we need to troubleshoot a problem while protecting their privacy.

1. Press Shift-Control-Option-Command-Period. Your screen will briefly flash.
2. After a few minutes, a Finder window will automatically open to `/private/var/tmp`
3. Send the most recent `sysdiagnose_DATE_TIME.tar.gz` file to your friendly developers.

The most important file in this archive is `system_logs.logarchive`, which will
include recent system logs including Blockstack's logs. You can open it on
a Mac using `Console.app`. The other files include information about your computer
that may help in diagnosing problems.

If you're worried about inadvertently sending some private information,
you can select the log entries you'd like to send inside `Console.app` and copy
them into an email or github issue.

More technical users (with admin permission) can use the `sysdiagnose` command
to generate a custom dump of information.

## Tech Stack（技术栈）

这个bloackstack使用最新的库和工具如下:

- [React Rocket Boilerplate](https://github.com/jakemmarsh/react-rocket-boilerplate)
- [ReactJS](https://github.com/facebook/react)
- [React Router](https://github.com/rackt/react-router)
- [RefluxJS](https://github.com/spoike/refluxjs)
- [Gulp](http://gulpjs.com/)
- [Browserify](http://browserify.org/)
- [Redux](https://github.com/reactjs/redux)
- [Babel](https://github.com/babel/babel)

Along with many Gulp libraries (these can be seen in either `package.json`, or at the top of each task in `/gulp/tasks/`).


## 测试部分

1. If you haven't already, follow steps 1 & 2 above
2. If you haven't already run `npm run dev` or `npm run build` at least once, run `npm run build`
3. Run all tests in the `tests/` directory with the `npm run test` command
  * A single file can be run by specifing an `-f` flag: `npm run test -f <PATH_TO_TEST_FILE>`
    * In the `PATH_TO_TEST_FILE`, it is possible to omit the `tests/` prefix, as well as the `.test.js` suffix. They will be automatically added if not detected.

*Note: When running tests, code coverage will be automatically calculated and output to an HTML file using the [Istanbul](https://github.com/gotwarlost/istanbul) library. These files can be seen in the generated `coverage/` directory.*
