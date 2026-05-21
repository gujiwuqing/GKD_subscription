# @gujiwuqing/GKD_subscription

> gujiwuqing 的 GKD 订阅规则，基于 AIsouler 的订阅 Fork 并持续维护。

---

## 订阅链接

复制以下任意一个链接到 GKD 即可使用本订阅规则：

### 推荐：jsDelivr CDN（国内速度快）

```txt
https://cdn.jsdelivr.net/npm/@gujiwuqing/gkd_subscription@latest/dist/gujiwuqing_gkd.json5
```

### GitHub Raw 源

```txt
https://raw.githubusercontent.com/gujiwuqing/GKD_subscription/main/dist/gujiwuqing_gkd.json5
```

### npm 官方源（备用）

```txt
https://registry.npmjs.org/@gujiwuqing/gkd_subscription/-/gkd_subscription-0.0.0.tgz
```

---

## 使用说明

- 仅默认启用 `开屏广告` 规则，其它规则需手动开启
- 建议按需开启规则，不要全部开启，避免规则阻塞和耗电增加
- 在 GKD 订阅界面下拉可检测更新

---

## 日常维护指南

### 项目结构

```
├── src/
│   ├── apps/              # 各 APP 的规则文件（如 com.luna.music.ts）
│   ├── subscription.ts    # 订阅元信息配置
│   ├── globalGroups.ts    # 全局规则组
│   ├── categories.ts     # 规则分类
│   └── globalDefaultApps.ts  # 全局规则默认启用的 APP 列表
├── dist/                  # 构建产物（自动生成，无需手动修改）
├── .github/workflows/     # CI 自动发布配置
├── package.json           # 项目配置
└── scripts/               # 构建和检查脚本
```

### 添加/修改规则

1. **编辑规则文件**：修改 `src/apps/` 下对应 APP 的 `.ts` 文件
2. **本地验证构建**：
   ```bash
   pnpm install    # 首次或依赖变更时执行
   pnpm run build  # 构建，检查是否有错误
   ```
3. **提交并推送**：
   ```bash
   git add -A
   git commit -m "feat: 描述你的修改"
   git push origin main
   ```
4. **自动发布**：推送后 CI 会自动触发 `build_release`，完成构建 → 发布到 npm → 同步到 CDN

### 手动触发发布

如果自动发布未触发，可以手动操作：

1. 打开 [Actions 页面](https://github.com/gujiwuqing/GKD_subscription/actions/workflows/build_release.yml)
2. 点击 **Run workflow** → 确认

### 获取 APP 快照（用于编写规则）

1. 在 GKD APP 中打开「高级模式」→ 「保存快照」
2. 在目标 APP 的目标页面触发保存
3. 导出 JSON 快照文件，分析节点树中的 `text`、`desc`、`id` 等属性
4. 编写对应的 GKD 选择器规则

### 规则编写要点

```typescript
// 使用 desc 属性匹配（汽水音乐 v19.0.0+ 等原生 UI）
matches: '[desc="领取奖励"][visibleToUser=true][focusable=true]'

// 使用 text 属性匹配（传统方式）
matches: '[text="跳过"][visibleToUser=true]'

// 使用 id 匹配（最稳定）
matches: '[id="com.example:id/btn_close"]'
```

---

## 发布相关配置

| 配置项 | 值 |
|--------|------|
| npm 包名 | `@gujiwuqing/gkd_subscription` |
| npm 主页 | https://www.npmjs.com/package/@gujiwuqing/gkd_subscription |
| GitHub 仓库 | https://github.com/gujiwuqing/GKD_subscription |
| CI Workflow | `.github/workflows/build_release.yml` |
| GitHub Secret | `NPM_TOKEN`（npm Granular Access Token，需有 publish 权限） |
| 自动发布时间 | 每天 UTC 19:00（北京时间凌晨 3:00）或手动触发 |

### 更新 NPM Token

Token 过期后需要更新：
1. 打开 https://www.npmjs.com/settings/gujiwuqing/tokens
2. 生成新的 **Granular Access Token**（勾选 Read and write + bypass 2FA）
3. 打开 https://github.com/gujiwuqing/GKD_subscription/settings/secrets/actions
4. 更新 `NPM_TOKEN` 的值

---

## 已适配规则

- 查看 [适配 APP 列表](./dist/README.md)
- 查看 [更新日志](https://github.com/gujiwuqing/GKD_subscription/releases)

## 参考资料

- [GKD 官网](https://gkd.li/) | [使用教程](https://gkd.li/guide/) | [API 文档](https://gkd.li/api/) | [常见问题](https://gkd.li/guide/faq)
- [规则编写教程](https://github.com/Snoopy1866/notebook/blob/main/04%20Others/GKD%20%E8%A7%84%E5%88%99%E7%BC%96%E5%86%99%E6%95%99%E7%A8%8B/gkd-rule-tutorial.md)
- [GKD 订阅模板](https://github.com/gkd-kit/subscription-template)
- [贡献指南](./CONTRIBUTING.md)

## 致谢

基于 [AIsouler/GKD_subscription](https://github.com/AIsouler/GKD_subscription) Fork 维护
