# tvbox-runtime

TVBox 爬虫运行时的打包产物，供 [`dyxia`](https://github.com/langziguilai/tvbox) 这类宿主按需下载。
由 `tools/build_runtime_packs.py` 生成，源仓库为 `dist/runtime/`。

## 目录结构

```
node/
  libnode-arm64-v8a.so.xz           # Node.js 原生库（xz 压缩）
  libnode-armeabi-v7a.so.xz
python/
  python-process-arm64-v8a.zip      # 独立进程版 CPython（libpython + stdlib + 依赖 + server.py）
  python-process-armeabi-v7a.zip
  native-arm64-v8a.zip              # Chaquopy 版原生库（可选）
  native-armeabi-v7a.zip
  requirements-arm64-v8a.zip        # Chaquopy 版 pip 依赖（可选）
  requirements-armeabi-v7a.zip
quickjs/
  libquickjs-wrapper-arm64-v8a.so.xz
  libquickjs-wrapper-armeabi-v7a.so.xz
```

## 作为下载源使用

启用 GitHub Pages 后，base url 为：

```
https://langziguilai.github.io/tvbox-runtime
```

宿主里对应配置：

- Node：`<base>/node/libnode-{abi}.so.xz`
- Python（独立进程）：`<base>/python`（自动拼接 `python-process-{abi}.zip`）
- QuickJS（可选下载模式）：`<base>/quickjs/libquickjs-wrapper-{abi}.so.xz`

也可以直接用 raw 地址：

```
https://raw.githubusercontent.com/langziguilai/tvbox-runtime/main
```

## 更新

```bash
python tools/build_runtime_packs.py     # 在 tvbox 仓库里重新生成 dist/runtime
cp -r dist/runtime/{node,python,quickjs} <this repo>/
git add -A && git commit -m "runtime: update packs" && git push
```
