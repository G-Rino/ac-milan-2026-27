# AC米兰 2026-2027 数据中心

纯静态、零前端外部请求的 AC 米兰赛季数据看板：赛程 / 赛果 / 积分榜 / 队内榜 / 数据分析（基础数据 + 队内数据王）。

- 数据源：直播吧（赛程赛果）、腾讯体育（积分榜 / 队内数据王 / 基础数据）、ESPN（队内进球助攻）
- 页面由本地脚本 `build_acmilan.py` 离线生成，浏览器打开后**不依赖任何运行时网络请求**。

## 本地预览
直接用浏览器打开 `index.html` 即可。

## 重新生成
    python3 build_acmilan.py

## 部署（手机随时查看）

### 方式 A：Netlify Drop（推荐，免实名）
1. 打开 https://app.netlify.com/drop （手机也能开）
2. 把本目录 **整个文件夹** 拖进去（不要只拖 index.html，连带 build_acmilan.py 一起也无妨）
3. 几秒后获得一个 `xxx.netlify.app` 网址，手机浏览器打开即可

更新数据后重新生成页面，再拖一次覆盖即可（或注册 Netlify 账号后连 Git 自动部署）。

### 方式 B：Gitee Pages（需实名 + 公开仓库）
推送到 Gitee **公开**仓库后，在仓库「服务 → Gitee Pages」选择「部署分支 + 根目录」启动，访问地址形如：
    https://你的用户名.gitee.io/仓库名/
注意：Gitee Pages 免费版不会随 push 自动更新，每次重新生成后需回页面点一次「更新」；首次使用需完成实名认证。

## 自动部署（仅数据变化时才上线）
`deploy_netlify.sh` 会先比对本次生成的 `ac-milan-site/.data_sig.txt` 与上一次发布记录 `ac-milan-site/.deployed_sig.txt`：
- 签名相同（只有"更新时间"变了，数据无实质变化）→ 自动跳过，不消耗 Netlify 部署额度；
- 签名不同（赛果 / 积分 / 队内数据有变）→ 自动发布新的 index.html + assets/ 到线上并记录新签名。

`build_acmilan.py` 每次都会重写本地两个 HTML 并刷新"更新时间"，但只有数据真的变化才会上线。
