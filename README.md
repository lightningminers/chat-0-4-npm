## 为什么要熟悉 NPM 相关的操作

npm 是伴随着 Node.js 成长的包管理器，最初它只服务于后端开发。早期前端相关的童鞋一直在用 bower 来做包管理，再更早的年代前端会用 Ant 来做管理和构建。

> 时间：2020年

对于一门编程语言的开发者而言，包管理（依赖管理）是一项考核该编程语言成熟度的重要标志，在解决多人协作，依赖管理上。

- 一次编写，多次安装复用
- 版本管理也非常方便

目前 NPM 做为事实的标准，不管你用其他任何的构建工具，如：webpack，rollup，parcel 等，或是想安装一个模块，大多数都能在 NPM 这个大仓库中找到，是的，这是中心化的。如果你想给社区贡献你的代码，你可以打包上传到 NPM，提供给开发者使用。

这就是我们为什么需要熟悉 NPM 相关操作的理由。

> 小提示：熟悉之后可以使用 yarn 来替代 npm，使用 nrm 来管理 npm 的源。

## 熟悉 NPM 相关的操作命令

这一部分主要来源于 [https://docs.npmjs.com/cli-documentation/](https://docs.npmjs.com/cli-documentation/)，我挑选了一些我们经常使用的命令，基本涵盖日常开发的 90% 。

> npm init

运行 `npm init -y` 会快速的创建一个 `package.json` 文件。

由于近年来 Cli 工具的流行，npm 提供了一个 `npm init  <@scope> (same as npx <@scope>/create)` 的命令，比如：

```bash
$ npm init react-app ./my-react-app
```

它将由npx安装 `create-react-app` 并启动一个 React 工程。

> npm install & npm uninstall

安装和卸载其实就是一对 `冤家`，它们必然是成对出现的。

常用的方式：

```bash
$ npm i xxx 或 npm r xxx
```

除此之外你还可以用 `tag`，`version` 的形式来安装指定的包。

如：

```bash
$ npm i react@16.8.5
```

在 install 中还有两个便捷的参数非常有用，它们是 `-p` 和 `-d`，分别会保存到 `package.json` 文件中的 `dependencies` 和 `devDependencies` 字段。

有时候我们需要安装内网 git 仓库上的包，可以通过这样的方式：

```bash
$ npm i https://github.com/indexzero/forever/tarball/v0.5.6
```

后缀可以用于控制安装的包版本（也就是 git tag），一共例举了几个方式，如：`gist`，`bitbucket`，`gitlab`，我想对于我们最常用的就是 `gitlab` 了。

```bash
$ npm i gitlab:mygitlabuser/myproject
```

对于开发本地包，可以使用 `file:` 的方式，如：

```json
{
  "dependencies": {
    "query": "file:./query"
  }
}
```

然后在当前目录执行 `npm i` 即可。

另外在额外提一嘴 `package-lock.json`，这是后期 npm 参考 yarn.lock 提供的一个机制，用于保证安装包时的依赖可以保持一致（多人协作时）。
 
> npm info

这是 `npm view` 的别名，用于查看一个包的详细属性等信息。

> npm outdated

此命令会列出所有已经过时的包。

> npm update

此命令会更新包

> npm adduser npm publish

一般这两个命令都是成对出现的，`adduser` 是登录 npm 账户，`publish` 是发布当前的包，当然出了发布外，你想安装私有的包，也是需要登录的。

既然说到了 `publish` 额外提一嘴 `.npmignore` 文件，这个文件和 `.gitignore` 文件的作用是相同的，我们可以设想一下，当你对外发布时将不想发布的内容发布了出去，这非常危险，这两个文件就可以控制哪个可以忽略。

> npm start npm stop npm build npm test

这些都是快捷命令，分别执行 `"scripts"` 中的 `start`，`stop`，`build` 和 `test`。

> npm help

这个命令也是我们很常用的，npm 的命令非常多和复杂，我们都不一定记得住，不过有 `help` 就帮我们解决这个问题。

```bash
$ npm help adduser
```

> npm dist-tag

当模块非常受欢迎时，对于更新作者一般都会发布 `alpha`，`beta` 等版本，这个时候 `dist-tag` 就非常有了，可以列出所有的 tag，如果你想当尝鲜的小白鼠，你就可以来看看对应最新的 tag（标签）。


> 小提示

还有一些命令如 `config`，`registry` 等或是 `.npmrc` 文件，这些并不常用，主要是针对 npm 配置相关，我们如果依赖到环境变量或者其他配置时，你就可以使用到这些。

比如我的 `.npmrc` 文件：

```
registry=https://registry.npmjs.org/
sass_binary_site=https://npm.taobao.org/mirrors/node-sass
```

`config` 命令就是用来配合修改配置的。


## 使用 link 在本地开发 JavaScript 包



## 思考

做为一个商业化中心化的平台，近年来关于安全方面的事故，发生了多起。这源于 JavaScript 生态的丰富，NPM 的注册机制并没有任何审核等。

想想著名的 `left-pad` 事件，导致很多不能用，当然后面 NPM 的做法是收回了删除的权限。还有一些是直接在代码中注入另外的脚本代码，我们可以将它看做木马，这个事情多数在和钱包相关的领域中被发现。

整体来看，在我们依赖开源项目的今天，安全这个事情，很值得我们去思考，我们该用什么机制，来至少保证依赖的安全性？

