---
id: 1h07un4d7qd57rle66ehzwd
title: Electron
desc: 'Notes on Electron'
updated: 1659801339075
created: 1659717564426
---
## General Info

Electron is a framework for creating native applications with Javascript, HTML and CSS.

## Preload Script

Electron's main process is a Node.js environment that has full operating system access. On top of [Electron modules](https://www.electronjs.org/docs/latest/api/app), you can also access [Node.js built-ins](https://nodejs.org/dist/latest/docs/api/), as well as any packages installed via npm. On the other hand, renderer processes run web pages and do not run Node.js by default for security reasons.

To bridge Electron's different process types together, we will need to use a special script called a preload.

## Inter Process Communication

Here is the [guide](https://www.electronjs.org/docs/latest/tutorial/ipc) and Here is the note [[devnotes.javascript.electron.inter-process-communication]]

## Context Isolation

Context Isolation is a feature that ensures that both your preload scripts and Electron's internal logic run in a separate context to the website you load in a webContents. This is important for security purposes as it helps prevent the website from accessing Electron internals or the powerful APIs your preload script has access to.

This means that the window object that your preload script has access to is actually a different object than the website would have access to. For example, if you set window.hello = 'wave' in your preload script and context isolation is enabled, window.hello will be undefined if the website tries to access it.

Context isolation has been enabled by default since Electron 12, and it is a recommended security setting for all applications.

Context Isolation means that preload scripts are isolated from the renderer's main world to avoid leaking any privileged APIs into your web content's code.

Instead, use the `contextBridge` module to accomplish this securely:

```javascript
// preload.js
const { contextBridge } = require('electron')

contextBridge.exposeInMainWorld('myAPI', {
  desktop: true,
})

// renderer.js
console.log(window.myAPI)
// => { desktop: true }
```

This feature is incredibly useful for two main purposes:

By exposing `ipcRenderer` helpers to the renderer, you can use [[inter-process communication]] **(IPC)** to trigger main process tasks from the renderer (and vice-versa).

If you're developing an Electron wrapper for an existing web app hosted on a remote URL, you can add custom properties onto the renderer's window global that can be used for desktop-only logic on the web client's side.

## Quick Tips

`win.webContents.openDevTools()` The BrowserWindow opens with Dev Tools Already Open
