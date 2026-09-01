# AC米兰 2026-2027 数据中心

纯静态、零前端外部请求的 AC 米兰赛季数据看板：赛程 / 赛果 / 积分榜 / 队内榜 / 数据分析（基础数据 + 队内数据王）。

- 数据源：直播吧（赛程赛果）、腾讯体育（积分榜 / 队内数据王 / 基础数据）、ESPN（队内进球助攻）
- 页面由本地脚本 `build_acmilan.py` 离线生成，浏览器打开后**不依赖任何运行时网络请求**。

## 本地预览
直接用浏览器打开 `index.html` 即可。

## 重新生成
    python3 build_acmilan.py

## 自动部署（仅数据变化时才上线）
`deploy_netlify.sh` 会先比对本次生成的 `ac-milan-site/.data_sig.txt` 与上一次发布记录 `ac-milan-site/.deployed_sig.txt`：
- 签名相同（只有"更新时间"变了，数据无实质变化）→ 自动跳过，不消耗 Netlify 部署额度；
- 签名不同（赛果 / 积分 / 队内数据有变）→ 自动发布新的 index.html + assets/ 到线上并记录新签名。

`build_acmilan.py` 每次都会重写本地两个 HTML 并刷新"更新时间"，但只有数据真的变化才会上线。
