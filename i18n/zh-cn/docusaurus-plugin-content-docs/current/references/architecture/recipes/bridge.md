---
title: Bridge
draft: true
---

import Rater from '@theme/Rater'
import useBaseUrl from '@docusaurus/useBaseUrl'

<div className="row">
  <div className="col col--4">
    <table>
      <tr>
        <td>Ease of Use</td>
        <td><Rater value="3"/></td>
      </tr>
      <tr>
        <td>可扩展性</td>
        <td><Rater value="5"/></td>
      </tr>
      <tr>
        <td>性能</td>
        <td><Rater value="4"/></td>
      </tr>
      <tr>
        <td>安全</td>
        <td><Rater value="4"/></td>
      </tr>
    </table>
  </div>
  <div className="col col--4 pattern-logo">
    <img src={useBaseUrl('img/recipes/Bridge.svg')} alt="Bridge" />
  </div>
    <div className="col col--4">
    Pros:
    <ul>
      <li>高度可配置</li>
      <li>无需 Rust 技能</li>
    </ul>
    Cons:
    <ul>
      <li>某些WebAPI不可用</li>
      <li>Challenge to implement</li>
    </ul>
  </div>
</div>

## 描述

The Bridge recipe is a secure pattern where messages are passed between brokers via an implicit bridge using the API. It isolates functionality to the specific scope and passes messages instead of functionality.

## Diagram

```mermaid
graph TD
  H==>F
  subgraph WEBVIEW
    F-.-E
  end
  D-->E
  E-->D
  B-->D
  D-->B
  subgraph RUST
    A==>H
    A-->B
    B-.-C
    B-.-G
  end
  A[Binary]
  B{Rust Broker}
  C[Subprocess 2]
  G[Subprocess 1]
  D(( API BRIDGE ))
  E{JS Broker}
  F[Window]
  H{Bootstrap}
  class D apibridge
  class RUST rust
  class WEBVIEW webview
```

## 配置

这里是您需要添加到 tauri.conf.json 文件中的内容：

```json
{
  "tauri": {
    "allowlist": {
      "all": false,
      "clipboard": {
        "all": false,
        "readText": false,
        "writeText": false
      },
      "dialog": {
        "all": false,
        "ask": false,
        "confirm": false,
        "message": false,
        "open": false,
        "save": false
      },
      "fs": {
        "all": false,
        "copyFile": false,
        "createDir": false,
        "readDir": false,
        "readFile": false,
        "removeDir": false,
        "removeFile": false,
        "renameFile": false,
        "scope": [],
        "writeFile": false
      },
      "globalShortcut": {
        "all": false
      },
      "http": {
        "all": false,
        "request": false,
        "scope": []
      },
      "notification": {
        "all": false
      },
      "os": {
        "all": false
      },
      "path": {
        "all": false
      },
      "process": {
        "all": false,
        "exit": false,
        "relaunch": false,
        "relaunchDangerousAllowSymlinkMacos": false
      },
      "protocol": {
        "all": false,
        "asset": false,
        "assetScope": []
      },
      "shell": {
        "all": false,
        "execute": false,
        "open": false,
        "scope": [],
        "sidecar": false
      },
      "window": {
        "all": false,
        "center": false,
        "close": false,
        "create": false,
        "hide": false,
        "maximize": false,
        "minimize": false,
        "print": false,
        "requestUserAttention": false,
        "setAlwaysOnTop": false,
        "setDecorations": false,
        "setFocus": false,
        "setFullscreen": false,
        "setIcon": false,
        "setMaxSize": false,
        "setMinSize": false,
        "setPosition": false,
        "setResizable": false,
        "setSize": false,
        "setSkipTaskbar": false,
        "setTitle": false,
        "show": false,
        "startDragging": false,
        "unmaximize": false,
        "unminimize": false
      }
    }
  }
}
```
