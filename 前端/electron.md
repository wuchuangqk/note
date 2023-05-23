# 官网

[Build cross-platform desktop apps with JavaScript, HTML, and CSS | Electron (electronjs.org)](https://www.electronjs.org/zh/)


# 官方脚手架forge

forge官网[Getting Started - Electron Forge](https://www.electronforge.io/)

# 创建项目

```sh
npm init electron-app@latest 项目名称
```



# 图标

| Operating system | Format  | Size                                           |
| ---------------- | ------- | ---------------------------------------------- |
| macOS            | `.icns` | 512x512 pixels (1024x1024 for Retina displays) |
| Windows          | `.ico`  | 256x256 pixels                                 |
| Linux            | `.png`  | 512x512 pixels                                 |

## 应用图标

```js
packagerConfig: {
  icon: './images/app-icon' // no file extension required
}
```

## 安装程序图标

```js
makers: [
    {
      name: '@electron-forge/maker-squirrel',
      config: {
        // The ICO file to use as the icon for the generated Setup.exe
        setupIcon: './images/setup-icon.ico',
      },
    },
]
```

# 打开控制台

```js
mainWindow.webContents.openDevTools();
// const mainWindow = new BrowserWindow();
```



# 进程间通信

electron分为主进程和渲染进程，主进程可以访问系统api，渲染进程只能渲染页面无法访问系统api。

## 仅发送通知事件

```js
// 渲染进程
ipcRenderer.send('set-title', title)

// 主进程
ipcMain.on('set-title', (event, title) => {
  const webContents = event.sender
  const win = BrowserWindow.fromWebContents(webContents)
  win.setTitle(title)
})
```



## 获取返回结果

```js
// 渲染进程
const res = await ipcRenderer.invoke('dialog:openFile')

// 主进程
ipcMain.handle('dialog:openFile', () => {
  const { canceled, filePaths } = await dialog.showOpenDialog()
  if (canceled) {
    return
  } else {
    return filePaths[0]
  }
})
```



# 安全



# 应用生命周期

## reday

## window-all-closed

## activate



# 预加载脚本

预加载（preload）脚本包含了那些执行于渲染器进程中，且先于网页内容开始加载的代码 。 这些脚本虽运行于渲染器的环境中，却因能访问 Node.js API 而拥有了更多的权限。
