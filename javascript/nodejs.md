---
title: Node.js
layout: default
parent: JavaScript
---

# Node.js

**Node.js 入门指南**

欢迎来到 Node.js 入门指南！Node.js 是一个可以在服务器端执行 JavaScript 的平台，让你可以使用 JavaScript 来创建高性能、高可扩展的 Web 应用。

**1. 什么是 Node.js?**
- 不是一个框架或库，而是一个运行时环境。
- 基于 Google 的 V8 JavaScript 引擎。
- 非阻塞 I/O 和事件驱动。

**2. 安装 Node.js**

访问 [Node.js 官网](https://nodejs.org/) 下载并安装合适的版本。安装完成后，你可以在命令行中使用 `node` 和 `npm`（Node 的包管理器）。

**3. 创建你的第一个 Node.js 应用**

创建一个名为 `app.js` 的文件：

```javascript
const http = require('http');

const server = http.createServer((req, res) => {
    res.writeHead(200, {'Content-Type': 'text/plain'});
    res.end('Hello Node.js!\n');
});

server.listen(3000, '127.0.0.1', () => {
    console.log('Server is running at http://127.0.0.1:3000/');
});
```

运行应用：

```shell
node app.js
```

在浏览器中访问 `http://127.0.0.1:3000/`，你会看到 "Hello Node.js!"。

**4. 使用 npm**

`npm` 是 Node.js 的包管理器，你可以使用它来安装、更新和管理库和工具。

例如，安装 `express`（一个流行的 Web 框架）：

```shell
npm install express
```

**5. 创建一个 Express 应用**

安装 Express 后，创建一个名为 `server.js` 的文件：

```javascript
const express = require('express');
const app = express();

app.get('/', (req, res) => {
    res.send('Hello from Express!');
});

app.listen(4000, () => {
    console.log('Server is running at http://127.0.0.1:4000/');
});
```

运行它：

```shell
node server.js
```

**6. 异步编程**

由于 Node.js 是单线程的，所以它使用回调、Promises 和 async/await 来处理异步。

例如，使用 Promise:

```javascript
const fs = require('fs').promises;

fs.readFile('file.txt', 'utf8').then(data => {
    console.log(data);
}).catch(error => {
    console.error('Error reading the file:', error);
});
```

**7. 更多核心模块**

Node.js 提供了许多有用的核心模块，如:
- `fs`: 文件系统。
- `path`: 处理文件和目录的路径。
- `os`: 提供操作系统相关的实用程序方法和属性。

**8. 更多资源**

- [Node.js 官方文档](https://nodejs.org/en/docs/)
- [NodeSchool](https://nodeschool.io/): 互动式教程

---

开始使用 Node.js 可能需要一些时间，但随着你更深入地探索它的功能和生态系统，你会发现它是一个非常强大和灵活的平台，适合各种应用和工作负载。