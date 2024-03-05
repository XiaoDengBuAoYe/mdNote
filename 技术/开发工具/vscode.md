### 配置

> 通过修改 c:/Users/用户名/AppData/Roaming/Code/User/settings.json 文件添加或修改配置

#### 其他

 在使用搜索功能时，将文件夹/文件排除在外
```
 "search.exclude": {
      "**/node_modules": true,
      "**/bower_components": true,
      "**/target": true,
      "**/logs": true,
}
```

 这些文件将不会显示在工作空间中
  ```
  "files.exclude": {
      "**/.git": true,
      "**/.svn": true,
      "**/.hg": true,
      "**/CVS": true,
      "**/.DS_Store": true,
      "**/*.js": {
          "when": "$(basename).ts" //ts编译后生成的js文件将不会显示在工作空中
      },
      "**/node_modules": true
  }
  ```

#### markdown

> 1.79 版本，提供了一项名为 Automatic copy of external files 的新功能，当用户使用拖拽或粘贴将外部媒体文件（比如图片、音视频）放置到 Markdown 文档上时，VSCode 会自动复制一份文件到工作区，并在 Markdown 文档中插入相应的图片引用片段。

##### 变量

- ${documentFileName} — Markdown 文档的完整文件名，比如 README.md
- ${documentBaseName} — Markdown 文档的基本文件名，比如 README
- ${documentExtName} — Markdown 文档的拓展名，比如 md
- ${documentDirName} — Markdown 文档的上级目录名词，比如示例的 api
- ${documentWorkspaceFolder} — Markdown 文档工作区路径，比如示例的 /Users/me/myProject。如果 Markdown 文档不是工作区的一部分，则该值与 ${documentDirName} 相同
- ${fileName} — 被拖拽或粘贴的图片文件名，比如 image.png

##### 配置项

- markdown.copyFiles.destination 配置控制图片文件的存放目录。value 则表示所匹配的这些 Markdown 文档，它们的图片文件存放目录，可以使用一些简单的变量.

  ```
  "markdown.copyFiles.destination": { 
      "**/*": "imgs/${documentBaseName}/" 
    }
  ```
  
  


### 拓展

- Chinese (Simplified) (简体中文) Language Pack for Visual Studio Code

  > 汉化 chajian

- HTML CSS Support

  > 前端支持

- Intellij IDEA Keybindings

  > idea 快捷键绑定
- live Server

  > 前端快速服务器
![alt text](imgs/vscode/image-2.png)
- One Dark Pro

  > 主题插件

- Prettier - Code formatter

  > 格式化 json css scss less vue 等

- Project Manager

  > 项目管理器

- Code Runner

  > python go 等程序快速执行

- Auto Rename Tag
  
  > 自动修改匹配的html标签

- stylelint

  > css/scss/less语法检查

- vetur
  
  > vue 语法高亮

- easy Less

  > less 保存时编译
#### MarkDown

- Markdown all in one

  > markdown 基础

- markdown preview enhanced

  > markdown实时预览

-
