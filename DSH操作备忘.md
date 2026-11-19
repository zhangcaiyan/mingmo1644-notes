# DSH 操作备忘

日常在 DeepSeek Harness 界面里用到的小操作，记一条算一条。

---

## 一、清空右侧栏（harness 标签）

右侧栏标签页乱了 / 想恢复默认布局 / 某个面板卡住打不开时用。

在 DSH 界面（本机 `http://127.0.0.1:19387`）按 **F12** 打开控制台，粘贴执行：

```js
Object.keys(localStorage).filter(k=>k.startsWith('dsh.sidebar-right')).forEach(k=>localStorage.removeItem(k));location.reload();
```

执行完页面自动刷新，右侧栏回到默认样式。

**它到底清的是什么**

- 存的是 `dsh.sidebar-right.v1.<sessionId>`：**每个会话各自一份**右侧栏布局——打开的标签页、当前选中项、左右分栏比例、浮动面板的矩形位置、标签身份计数都在里面，值是 JSON。
- 所以只影响右侧栏的"摆法"：会话内容、对话记录、左侧、主题等其他设置都不动。
- 清完页面会重载；因为找不到该会话的存档，右侧栏按默认重新开始（展开时种入默认页）。

**几个注意点**

1. 只清**当前 origin** 的存储；换端口、换浏览器（或 Electron 应用与浏览器之间）要分别清。
2. 左侧的浏览器页签是另一个键 `dsh.sidebar-browser.v1`，这条脚本不动它。想一起清，把 `sidebar-right` 改成 `sidebar`。
3. 只想清某一个会话：先跑 `Object.keys(localStorage).filter(k=>k.startsWith('dsh.sidebar-right'))` 看一眼有哪些 key，再把 filter 换成 `k === '那个完整的键'`。

## 二、待补

用到再记。
