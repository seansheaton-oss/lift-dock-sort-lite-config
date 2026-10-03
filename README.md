# Lift Dock Sort Lite — Privacy & Ads Configuration

Developer: Jocelyn  
Contact: seansheaton@gmail.com  
Android package: `com.liftdock.sortlite`

## Public URLs

- Privacy policy: https://seansheaton-oss.github.io/lift-dock-sort-lite-config/
- Remote configuration: https://seansheaton-oss.github.io/lift-dock-sort-lite-config/ads.json

## 切换测试 / 正式广告

编辑本仓库根目录 `ads.json`，只修改 `mode`：

- `"mode": "test"`：五个奖励点位全部使用 Google 官方测试 Rewarded ID。
- `"mode": "production"`：使用 `production_rewarded_units` 中各点位的正式 ID。

每次修改同时增加 `revision`（例如 1 → 2），然后 Commit changes。初始模式为 test，不根据日期、设备或审核人员自动切换。GitHub Pages 部署及 CDN 更新需要时间，修改并非立即到达所有客户端。

App ID 固定为 `ca-app-pub-5210982448594117~2091242561`；测试/正式切换仅选择广告单元，不在运行中更换 App ID。不要将 App ID 的 `~` 写成广告单元的 `/`。

只有有仓库写入权限的人可以修改配置；公开页面没有全局切换按钮，也不放置 GitHub token 或私钥。访客读取配置不需要登录。

## 当前接入状态

此仓库负责托管隐私政策和远程配置。当前已交付的游戏 APK 仍是离线 Mock 广告，尚未接入真实 AdMob SDK 和此配置地址。修改 JSON 不会改变旧 APK 的广告。完成客户端接入后，同一个接入版 APK 才可按远程配置切换，不需要再次安装。

接入约定：默认测试；仅接受 schema_version=1、匹配包名、test/production 两种 mode 和完整有效 ID；网络失败/配置不合法不自动启用正式广告；配置切换不得影响已经展示中的广告或重复发放奖励。

Google 测试广告仍通过 Google SDK 联网，与 Mock 广告不同。测试/正式切换不绕过用户同意或隐私披露。正式发布前应核对实际 SDK 和 Play Data safety 信息；Google 官方建议发布版本使用自己的广告单元。

## GitHub Pages

Settings → Pages → Deploy from a branch → main → /(root) → Save。`index.html` 为公开政策，`ads.json` 为配置，`.nojekyll` 禁用 Jekyll 处理。

## References

- https://developers.google.com/admob/android/test-ads
- https://developers.google.com/admob/android/quick-start
- https://developers.google.com/admob/android/privacy/play-data-disclosure
- https://policies.google.com/privacy
- https://docs.github.com/en/site-policy/privacy-policies/github-general-privacy-statement
