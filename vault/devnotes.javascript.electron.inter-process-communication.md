---
id: cOSLT6ncEiScjLx1bEQKH
title: Inter Process Communication
desc: ''
updated: 1659802084950
created: 1644000860449
---

## General Info

Inter-process communication (IPC) is a key part of building feature-rich desktop applications in Electron. Because the main and renderer processes have different responsibilities in Electron's process model, IPC is the only way to perform many common tasks, such as calling a native API from your UI or triggering changes in your web contents from native menus.

### IPC Channels

In Electron, processes communicate by passing messages through developer-defined "channels" with the ipcMain and ipcRenderer modules. These channels are arbitrary (you can name them anything you want) and bidirectional (you can use the same channel name for both modules).
