# ClashRule

本仓库用于维护 FlClash / Mihomo 使用的 Clash 规则，并提供兼容普通 `.list` 转换工具的主配置。

仓库不包含订阅链接、节点密码、密钥等敏感信息。

## 当前规则源

以下 4 个 `.list` 是当前活动规则源：

| 文件 | 用途 |
|---|---|
| `Clash_AI.list` | AI 服务规则 |
| `Clash_Ban.list` | 广告、统计和拦截规则 |
| `Clash_Proxy.list` | 自动代理规则 |
| `Clash_Direct.list` | 自定义直连规则 |

补充文件：

| 文件 | 用途 |
|---|---|
| `China_Domain_Extra.list` | 补充 China_Domain 缺少的 `cn`、`ms` 规则 |
| `YihaoShequ.list` | 一号社区拦截规则 |
| `Clash.ini` | Subconverter 风格的转换主配置 |

`rules/` 目录中的 `Clash_*_20260913.yaml` 仅作为历史快照保留，不再维护。

## 使用方式

### 方式一：使用转换工具

1. 使用转换工具加载 `Clash.ini`。
2. 输出目标选择 FlClash、Clash 或 Mihomo。
3. 将生成的 YAML 配置导入 FlClash。

注意：`Clash.ini` 不是 FlClash 可直接导入的完整配置，需要先经过转换工具生成 YAML。

### 方式二：直接引用 `.list`

支持 classical 规则集的 Clash / Mihomo 客户端，可以引用本仓库的 GitHub Raw 地址，例如：

```text
https://raw.githubusercontent.com/wiihunting/ClashRule/main/Clash_AI.list
```

规则集建议配置为：

```yaml
behavior: classical
format: text
```

## 当前规则顺序

规则按从上到下匹配，当前主配置大致保持以下顺序：

1. BlockHttpDNS
2. 局域网直连
3. 酒店登录弹窗测试规则
4. 广告和拦截规则
5. AI 规则
6. Google、Apple、Microsoft
7. 自定义代理和 Google 代理
8. 国内直连
9. YouTube
10. Twitter
11. OnDemand、Nippon
12. 中国域名和 IP 直连
13. `FINAL`

关键顺序不要随意调整，尤其是：

- `dash.cloudflare.com` 必须位于 `cloudflare.com` 之前。
- AI 必须位于 Microsoft 和普通代理规则之前。
- Ban 规则必须位于 Google、Microsoft 等代理规则之前。
- China 直连和 `GEOIP,CN` 应位于 `FINAL` 之前。

## 规则说明

- `.list` 使用普通文本规则格式，支持 `#` 注释和注释掉的规则。
- blackmatrix7 的规则优先使用其 `rule/Clash/<名称>/<名称>.list` 版本，以保留 IPv6、`PROCESS-NAME` 等规则。
- Grok 相关域名归入 `🤖 AI`。
- Twitter 使用 `🐦 Twitter` 分组。
- `Clash.ini` 不使用 `clash-classic:` 或 `clash-domain:`，以兼容只支持普通 `.list` 的转换工具。

## 维护约定

- 修改活动规则前，先保留上一天的历史快照。
- 规则文件和主配置修改后，本地与 GitHub 必须保持一致。
- 历史快照只用于留档，不继续修改。
- 新增或修改 `.list` 后，使用转换工具实际转换一次，确认规则被正确带入。
- 不写入订阅地址、节点密码、Token 或私钥。

## 历史快照

带日期的文件只用于记录历史版本，例如：

```text
Clash_AI_20260913.yaml
Clash_Ban_20260913.yaml
Clash_Proxy_20260913.yaml
Clash_Direct_20260913.yaml
Clash_20260913.ini
Clash_20260912.ini
```

当前规则以无日期的 `.list` 文件为准。
