---
id: 1h07un4d7qd57rle66ehzwd
title: Electron
desc: 'Notes on Electron'
updated: 1659754943983
created: 1659717564426
---
## General Info

Electron is a framework for creating native applications with Javascript, HTML and CSS.

## Preload Script

Electron's main process is a Node.js environment that has full operating system access. On top of [Electron modules](https://www.electronjs.org/docs/latest/api/app), you can also access [Node.js built-ins](https://nodejs.org/dist/latest/docs/api/), as well as any packages installed via npm. On the other hand, renderer processes run web pages and do not run Node.js by default for security reasons.

To bridge Electron's different process types together, we will need to use a special script called a preload.

## Inter Process Communication

Here is the [guide](https://www.electronjs.org/docs/latest/tutorial/ipc)
