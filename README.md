## 创建项目

```
hexo init Vocabularies
```

```
cd Vocabularies
```

```
cnpm i
```

## 使用[Tranquilpeak](https://github.com/LouisBarranqueiro/hexo-theme-tranquilpeak/tree/main)主题

1. Download the latest [version](https://github.com/LouisBarranqueiro/hexo-theme-tranquilpeak/archive/main.zip)

2. Rename the folder in `tranquilpeak` and place it in the `themes` folder of your Hexo blog

3. Modify the theme in Hexo configuration file (`_config.yml`) by setting `theme` variable to `tranquilpeak`

4. Go to the `tranquilpeak` folder and run `npm install && npm run prod`

5. Read [documentation](https://github.com/LouisBarranqueiro/hexo-theme-tranquilpeak/blob/main/DOCUMENTATION.md) to configure the theme.

    

    

1. 切换到`H:\Github\Vocabularies\themes\tranquilpeak`：
    ```
    cnpm i
    ```
    ```
    npm run prod
    ```

2. 切换到`H:\Github\Vocabularies`本地预览：
     ```
     hexo s
     ```

#### 修改主题相关内容

样式：`H:\Github\Vocabularies\themes\tranquilpeak\source\_css\utils\mixins/_sidebar.scss`

生成的样式：

`H:\Github\Vocabularies\themes\tranquilpeak\source\assets\css/style.css`

样式变量：`H:\Github\Vocabularies\themes\tranquilpeak\source\_css\utils/_variables.scss`

修改了主题的相关样式或设置，要重新切换到`H:\Github\Vocabularies\themes\tranquilpeak`：运行：

```
npm run prod
```

`每次修改了主题的相关内容，都要重新执行npm run prod`

#### [显示分类、标签和归档的操作](https://github.com/LouisBarranqueiro/hexo-theme-tranquilpeak/blob/main/DOCUMENTATION.md#enable-pages)

> 注：这3个页面一定要加`layout: `字段，如：`layout: "all-categories"`，如果不加上，点击页面不显示分类/标签/归档

#### Enable all-categories page

To enable `all-categories` page:

1. Run `hexo new page "all-categories"`. A new folder named `all-categories` will be created in `source/`
2. Replace `source/all-categories/index.md` content with:

```
---
title: "all-categories"
layout: "all-categories"
comments: false
---
```

This page will be reachable at: `/all-categories`. On this page, users will be able to search and filter posts by categories.

#### Enable all-tags page

To enable `all-tags` page:

1. Run `hexo new page "all-tags"`. A new folder named `all-tags` will be created in `source/`
2. Replace `source/all-tags/index.md` content with:

```
---
title: "all-tags"
layout: "all-tags"
comments: false
---
```

This page will be reachable at: `/all-tags`. On this page, users will be able to search and filter posts by tags.

#### Enable all-archives page

To enable `all-archives` page:

1. Run `hexo new page "all-archives"`. A new folder named `all-archives` will be created in `source/`
2. Replace `source/all-archives/index.md` content with:

```
---
title: "all-archives"
layout: "all-archives"
comments: false
---
```

This page will be reachable at: `/all-archives`. On this page, users will be able to search and filter posts by date.
**Search pattern** : YYYY/MMM/DD

#### 添加favicon

1. 将图片放在`H:\Github\Vocabularies\themes\tranquilpeak\source\_images`，执行`npm run prod`命令，图片会自动生成到`H:\Github\Vocabularies\themes\tranquilpeak\source\assets\images`

2. 在项目目录（`H:\Github\Vocabularies`）执行`hexo g`，把生成的`public`目录里的内容放到网站目录

### 【修改样式表的路径为相对路径--可忽略】

根据控制台显示的`Running "replace:linker" (replace) task`，找到`H:\Github\Vocabularies\themes\tranquilpeak\tasks\config\sails-linker.js`修改生成css的路径

修改`fileTmpl`字段，

```
devCss: {
  options: {
    // fileTmpl: '<%- css(\'./%s\') EJS_ENDTAG',
    fileTmpl: '<link rel="stylesheet" href="./%s">',
  },
  files: {
    'layout/_partial/head.ejs': pipeline.tranquilpeakCssFilesToInject
  }
},

prodCss: {
  options: {
    // fileTmpl: '<%- css(\'./%s\') EJS_ENDTAG',
     fileTmpl: '<link rel="stylesheet" href="./%s">',
  },
  files: {
    'layout/_partial/head.ejs': 'source/assets/css/*.min.css'
  }
}
```

然后重新执行`npm run prod`

`H:\Github\Vocabularies\themes\tranquilpeak\layout\_partial\head.ejs`中的`<%- css('assets/css/style-ec10xb65gu3othzfvkocyihllqgnzgrhyuvihqnqouoirvp93v2hmf8uhrqr.min.css') %>`变成`  <link rel="stylesheet" href="./assets/css/style-vysp8yst3qlbzrtwbqkxtjn2llqfuewkmedmattsd0fvl8kemoniaqrajh9v.min.css">`

#### js路径同理

```
// fileTmpl: '<%- js(\'%s\') EJS_ENDTAG',
fileTmpl: '<script src="./%s"></script>',
```

#### 修改图片路径

`H:\Github\Vocabularies\themes\tranquilpeak\layout\_partial\cover.ejs`：

```
<!-- coverImageUrl = url_for('./' +  theme.image_dir + '/' + theme.cover_image); -->
coverImageUrl = './' +  theme.image_dir + '/' + theme.cover_image;
```

#### 修改页面的访问路径为相对路径

`H:\Github\Vocabularies\themes\tranquilpeak\layout\_partial\sidebar.ejs`：

```
link.absolute_url = '.' + link.url;

<a
    class="sidebar-button-link <%= link.class %>"
    href="<%- link.absolute_url %>"
>
```

`修改为相对路径，是因为放到GitHub中的新仓库中，使用https://winney07.github.io/Vocabularies/访问，如果不改为相对路径，会默认是https://winney07.github.io/下的路径`

`出现问题1`：

在访问https://winney07.github.io/Vocabularies/all-categories/时，页面样式和图片等错误，因为是使用相对链接的，所以直接将这些静态资源的路径改为绝对地址：

`sails-linker.js`

```
fileTmpl: '<script src="https://winney07.github.io/Vocabularies/%s"></script>',

fileTmpl: '<link rel="stylesheet" href="https://winney07.github.io/Vocabularies/%s">',
```

`cover.ejs`

```
coverImageUrl = 'https://winney07.github.io/Vocabularies/' +  theme.image_dir + '/' + theme.cover_image;
```

`问题2`：

当访问https://winney07.github.io/Vocabularies/all-categorie时，再点击`tags`	导航时，切换到https://winney07.github.io/Vocabularies/all-categories/all-tags

所以，导航路径也设置为绝对路径

`sidebar.ejs`：

```
link.absolute_url = 'https://winney07.github.io/Vocabularies' + link.url;
```

> 以上修改相对路径，是针对将项目部署到GitHub仓库（非gitpages原始仓库），使用GitHub链接访问而做的

## 部署到GitHub

1. 修改根目录的`_config.yml`

   ```
   deploy:
     type: 'git' #部署的类型
     repository: git@github.com:winney07/Vocabularies.git   #仓库地址
     branch: main   #分支名称    
     ——————hexo d的代码是部署到main分支里面的(而博客的链接就是访问main分支里面的内容),即博客的内容
   ```


2. 提交到远程仓库

    ```
    hexo clean
    hexo g
    hexo d
    ```

    报错：

    ```
    INFO  Validating config
    ERROR Deployer not found: git
    ```

    **解决：**

    ```
    cnpm i --save hexo-deployer-git
    ```

    然后再执行`hexo d`

3. 在新创建的仓库中，选择`“Setting"——>”Pages"——>"**Branch**"选择"main"(选择网页所在分支)`

4. 最后访问地址：https://winney07.github.io/Vocabularies

5. 使用Custom domain（自定义域名）访问【因为使用https://winney07.github.io/Vocabularies访问，需要修改的相对路径太多了，而且好麻烦】

    在Custom domain中填写自定义域名，保存后即可。

6. 将`Enforce HTTPS `勾选

6. 新建自定义域名时：
    ```
    1. 记录类型：CNAME
    2. 主机记录：vocabularies
    3. 记录值：winney07.github.io（填写cname指向的域名）
    ```


​        https://vocabularies.winney07.cn/

### 将项目源文件提交到GitHub

1. ### 创建分支hexo（用于存放博客的源文件） [参考教程](https://www.cnblogs.com/kaerxifa/p/11045573.html)

    ```
    git branch hexo
    ```

    终端报错：`fatal: not a git repository (or any of the parent directories): .git`

    **解决：**

    1. 创建`.git`目录

        ```
        git init    // **如果在一个没有.git文件夹的目录下报上面这个错**，就执行这句
        ```

    2. 再重新创建新分支

        ```
        git checkout -b new-branch    // 可以使用这个命令也可以使用原来的
        ```

2. ### 将内容从工作目录添加到暂存区

    ```
    git add .
    ```

    执行`git add.`代码，报错：

    ```
    warning: adding embedded git repository: .deploy_git
    hint: You've added another git repository inside your current repository.
    hint: Clones of the outer repository will not contain the contents of
    hint: the embedded repository and will not know how to obtain it.
    hint: If you meant to add a submodule, use:
    hint:
    hint:   git submodule add <url> .deploy_git
    hint:
    hint: If you added this path by mistake, you can remove it from the
    hint: index with:
    hint:
    hint:   git rm --cached .deploy_git
    hint:
    hint: See "git help submodule" for more information.
    ```

    **解决：**

    1. 要在项目根目录添加`.gitignore`：

       ```
       .DS_Store
       Thumbs.db
       db.json
       *.log
       node_modules/
       public/
       .deploy*/        // 不要把deploy相关的提交
       ```

    2. 撤销刚才的添加

       ```
       git reset
       ```

    3. 重新提交代码

       ```
       git add .
       ```

3. ### 将更改记录（提交）到存储库（新分支）

    ```
    git commit -m 'vocabularies源码'
    ```

4. ### 推送到新分支到GitHub

    ```
    git push origin hexo
    ```

    报错：

    ```
    fatal: 'origin' does not appear to be a git repository
    fatal: Could not read from remote repository.
    
    Please make sure you have the correct access rights
    and the repository exists.
    ```

    **解决：**

    1. 确认本地仓库中是否已经配置了名为 `origin` 的远程仓库

       ```
       git remote -v
       ```

    2. 如果您没有看到名为 `origin` 的远程仓库，您需要将其添加到本地仓库中：

       ```
       git remote add origin git@github.com:winney07/Vocabularies.git
       ```

    3. 添加远程仓库后，再次尝试执行 `git push origin hexo` 命令

### 当前分支 `hexo` 没有与远程分支建立关联

当本地修改了内容，执行`git add .`，`git commit -m '修改备注'`，`git push` ，会报这样的错：

```
fatal: The current branch hexo has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin hexo

To have this happen automatically for branches without a tracking
upstream, see 'push.autoSetupRemote' in 'git help config'.
```

> **这个错误表明当前分支 `hexo` 没有与远程分支建立关联**



方法1：

```
git push --set-upstream origin hexo
```

> 以后的推送操作中，直接使用 `git push` 而不需要指定远程仓库和分支了

方法2：也可以通过配置 `push.default` 来自动设置跟踪分支

```
git config push.default current
```

