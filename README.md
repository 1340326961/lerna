# Lerna是一个管理工具，用来管理多个软件包（package）的javascript项目。

## 工作的两种模式
1. Fixed/Locked mode (default)
    在 pushlish 的时候，lerna.json 文件里面 "version": "0.1.5", 
    依据这个号，进行增加，‘只选择一次’，其他有改动的包自动更新版本号。

2. Independent mode
    lerna.json 文件里面 "version": "independent"
    每次publish时，都将得到一个提示符，提示每个已更改的包，以指定是补丁、次要更改、主要更改还是自定义更改。（各选各的版本号）

## 1. 初始化lerna项目

```js
lerna notice cli v4.0.0     // 版本号
lerna info Initializing Git repository  // 初始化git仓库
lerna info Creating package.json        // 创建package.json
lerna info Creating lerna.json          // 创建lerna.json
lerna info Creating packages directory  // 创建packages目录
lerna success Initialized Lerna files   // 初始化成功
```
## set up
npm + git
    git: git remote add origin https://github.com/1340326961/lerna.git
    npm: npm login - 用户名 - 密码 - 邮箱 

yarn + workspaces模式
    每个子包中都会有 node_modules ， 通过这样设置后，只有顶层有一个node_modules

```
    # package.json 文件加入

    "workspaces": [
        "packages/*"
    ],

    # lerna.json 文件加入

    "useWorkspaces": true,
    "npmClient": "yarn",
```
## Lerna Script

### lerna create < name > [loc]
    创建一个包
    name: 包名
    loc: 位置
```
    # 根目录的package.json 
    "workspaces": [
        "packages/*",
        "packages/@gp0320/*"
    ],
    
    # 创建一个包gpnote默认放在 workspaces[0]所指位置
    lerna create gpnote 

    # 创建一个包gpnote指定放在 packages/@gp0320文件夹下，注意必须在workspaces先写入packages/@gp0320，看上面
    lerna create gpnote packages/@gp0320
```
### lerna add [@version] [--dev] [--exact]
    增加 本地 或 远程 package做为当前项目packages里面的依赖

   1. --dev devDependencies 替代 dependencies
   2. 安装准确版本，就是安装的包版本前面不带^

```
    将 axios 包添加到“packages”下的包中 在开发环境
    lerna add axios packages/* --dev

    安装 module-1 到 module-2
    lerna add module-1 --scope=module-2 --dev

    在除 module-1 之外的所有模块中安装 module-1
    lerna add module-1

    在所有模块中安装 modules
    lerna add babel-core
```

### lerna bootstrap
    默认是npm i,因为我们指定过yarn，所以用的是 yarn install,会把所有包的依赖安装到根node_modules.
    且会让你可以 在 require() 中直接通过软件包的名称进行加载，就好像此软件包已经存在于 你的 node_modules 目录下一样。

### lerna list
    列出所有的包，如果与你文夹里面的不符，进入那个包运行yarn init -y解决
    ```
    daybyday
    gpnode
    gpwebpack
    temp
    lerna success found 4 packages
    ```

### lerna import

    导入本地存在的包

### lerna run
    ```
        lerna run < script > -- [..args] # 运行所有包里面的有这个script的命令
        $ lerna run --scope my-component test   #单个包的 test
    ```
### lerna link

    项目包建立软链，类似npm link

### lerna clean

    删除所有包的node_modules目录
    
### lerna changed
    列出下次发版lerna publish 要更新的包。













