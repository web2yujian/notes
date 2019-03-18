webpack打包时报错：throw er; // Unhandled 'error' event 解决方案



```
PS E:\www\Web\Vue.js\my-todo> npm run dev

> my-todo@1.0.0 dev E:\www\Web\Vue.js\my-todo
> cross-env NODE_ENV=development webpack-dev-server --config webpack.config.js --mode development

events.js:167
      throw er; // Unhandled 'error' event
      ^

Error: listen EADDRINUSE: address already in use 0.0.0.0:8088
    at Server.setupListenHandle [as _listen2] (net.js:1290:14)
    at listenInCluster (net.js:1338:12)
    at doListen (net.js:1471:7)
    at process._tickCallback (internal/process/next_tick.js:63:19)
    at Function.Module.runMain (internal/modules/cjs/loader.js:745:11)
    at startup (internal/bootstrap/node.js:283:19)
    at bootstrapNodeJSCore (internal/bootstrap/node.js:743:3)
Emitted 'error' event at:
    at emitErrorNT (net.js:1317:8)
    at process._tickCallback (internal/process/next_tick.js:63:19)
    [... lines matching original stack trace ...]
    at bootstrapNodeJSCore (internal/bootstrap/node.js:743:3)
npm ERR! code ELIFECYCLE
npm ERR! errno 1
npm ERR! my-todo@1.0.0 dev: `cross-env NODE_ENV=development webpack-dev-server --config webpack.config.js --mode development`
npm ERR! Exit status 1
npm ERR!
npm ERR! Failed at the my-todo@1.0.0 dev script.
npm ERR! This is probably not a problem with npm. There is likely additional logging output above.

npm ERR! A complete log of this run can be found in:
npm ERR!     C:\Users\10482\AppData\Roaming\npm-cache\_logs\2019-03-14T12_33_23_726Z-debug.log
```



后来发现是前面已经运行过一个服务;器（我的是`webpack-dev-server`）;端口被占用，**关闭原来的服务，或者换一个端口就好了**

