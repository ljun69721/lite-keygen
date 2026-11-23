# Keil Keygen Web（复刻版）

一个零依赖、纯静态的前端序列号生成器：淡绿白配色、卡片布局。选择目标平台与许可类型，
填写设备标识（Computer ID），即可在浏览器内生成并复制 6 组、35 个字符的序列号。

- 支持 **C51 / C251 / C166 / ARM** 四个平台、**11 种许可**。
- 所有计算在浏览器 Web Worker 中完成，**无后端、不上传任何数据**。
- 生成器在 Worker 中复用同一随机流，连续生成结果不同；修改设备信息会自动清空旧结果。

## 本地预览

需要 Node.js 20+，无需 `npm install`：

```powershell
node tools/preview.mjs
```

然后浏览器访问 <http://127.0.0.1:4173/>（端口被占用时：`$env:PORT='4174'; node tools/preview.mjs`）。

> 页面使用 ES modules 和 Web Worker，必须通过 HTTP(S) 访问，不能直接双击打开 `site/index.html`。

## 测试

```powershell
node --test tests/core.test.mjs
```

## 结构

```text
keil-keygen/
├─ site/                      # 可直接作为静态站点发布
│  ├─ index.html              # 页面结构
│  ├─ styles.css              # 淡绿主题样式
│  ├─ app.mjs                 # 表单 / 结果 / 复制交互
│  ├─ session.mjs             # 会话状态机：参数变更清结果、丢弃过期响应
│  ├─ generator.worker.mjs    # Web Worker：承载生成计算
│  ├─ core.mjs                # 生成算法（旧式 MT19937 + 分段校验编码）
│  └─ favicon.svg
└─ tools/preview.mjs          # 零依赖本地静态服务器
```

## 部署到 GitHub Pages

把 `site/` 目录作为发布源即可（GitHub Actions「Deploy from branch / static」或任意静态托管）。
资源全部使用相对路径，可部署在仓库子路径下。

## 说明

本项目由低空飞行器协会维护，作为纯前端序列号生成工具的技术实现，仅供学习与研究使用。
