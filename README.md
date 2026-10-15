# singbox-rules

自用 sing-box 规则集（rule-set）。`source/` 下是 JSON 源文件，仓库根目录是编译好的 `.srs` 二进制规则集。

| 规则集 | 内容 | 用途 |
| --- | --- | --- |
| `karpov.srs` | `karpov.cn` 及其全部子域名（`*.karpov.cn`） | 走代理 |

## 使用

```json
{
  "route": {
    "rule_set": [
      {
        "tag": "karpov",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/MiChongs/singbox-rules/main/karpov.srs",
        "update_interval": "1d"
      }
    ],
    "rules": [
      { "rule_set": "karpov", "outbound": "proxy" }
    ]
  }
}
```

国内网络可以在地址前面加镜像前缀，例如 `https://v6.gh-proxy.org/https://raw.githubusercontent.com/...`。

## 修改规则

编辑 `source/*.json` 之后重新编译，并把源文件和 `.srs` 一起提交：

```sh
sing-box rule-set compile --output karpov.srs source/karpov.json
sing-box rule-set match -f binary karpov.srs console.karpov.cn   # 验证
```
