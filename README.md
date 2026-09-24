# 流水宴 · 品牌官网

“流水有意，佳肴成席”——一个无需构建工具、可以直接发布到 GitHub Pages 的中文宴席品牌网站。

## 网站功能

- 30 道菜，六大分类，每道菜均有仓库内置的独立高清美食图、搜索、筛选和菜品详情
- 菜篮：加入、加减数量、删除、清空、自动合计
- “一键配一桌”：按人数生成荤素汤甜搭配
- 宴席预订：日期、时间、人数、座位偏好；同一浏览器只可预订一次
- 可选 Supabase 云端计数，让不同手机看到同一个真实预订人数
- 本地评价、收藏、夜宴模式、移动端菜单、滚动动画和无障碍键盘支持
- 隐藏订阅管理页 `liushui-console-7c9f.html`，可查看邮箱并导出 CSV（不出现在官网导航）
- 所有路径均为相对路径，适配 GitHub Pages 项目子目录
- 不使用外部 CDN，不依赖 npm，国内网络也能完整打开静态内容

## 本地预览

直接双击 `index.html` 即可。推荐在文件夹内运行：

```bash
python3 -m http.server 8080
```

然后访问 `http://localhost:8080`。

## 发布到 GitHub Pages

1. 新建 GitHub 仓库并上传本文件夹内的全部文件。
2. 打开仓库的 **Settings → Pages**。
3. 在 **Build and deployment** 选择 `Deploy from a branch`，分支选择 `main`，目录选择 `/ (root)`。
4. 保存，等待几分钟后打开 GitHub 给出的地址。

## 开启全班共享的真实预订人数（可选）

纯 GitHub Pages 没有数据库，因此默认只在本浏览器保存预订。若要跨手机实时共享：

1. 免费注册 Supabase，新建项目。
2. 在 SQL Editor 运行 `supabase/setup.sql`。
3. 在 Project Settings → API 复制 Project URL 与 anon public key。
4. 编辑 `config.js`：

```js
window.LSY_CONFIG = {
  SUPABASE_URL: "https://你的项目.supabase.co",
  SUPABASE_ANON_KEY: "你的 anon key"
};
```

5. 重新上传 `config.js`。页面的人气卡会自动显示“云端实时”，同一设备重复预订会被数据库拒绝。

订阅邮箱也会使用同一个 Supabase 项目保存。管理页面地址为：

```text
https://你的用户名.github.io/你的仓库名/liushui-console-7c9f.html
```

这个页面已设置为不让搜索引擎收录，但任何知道完整链接的人都能访问，适合课堂演示，不适合保存敏感资料。

> `anon key` 是专门给网页公开使用的公共密钥，不要填写 `service_role` 密钥。

## 修改菜单

菜品数据全部在 `script.js` 顶部的 `DISHES` 数组中。可改名称、价格、介绍、分类、颜色和图案符号。

## 项目结构

```text
.
├── index.html
├── liushui-console-7c9f.html
├── styles.css
├── script.js
├── config.js
├── config.example.js
├── assets/
│   ├── menu/             # 30 张菜品图
│   └── images/           # 3 张宴席场景图
├── supabase/setup.sql
├── .nojekyll
├── LICENSE
└── README.md
```
