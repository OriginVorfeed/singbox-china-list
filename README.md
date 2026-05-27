# singbox-china-list

你好，欢迎来到 Vorfeed 的欢乐满满翻墙提高班。

本项目是 **SmartDNS、Xray、Shadowrocket、sing-box** 统一分流规则的一部分，通过严格同步 [dnsmasq-china-list](https://github.com/felixonmars/dnsmasq-china-list)，保证多端分流规则的一致性。

- SmartDNS 规则：[smartdns-china-list](https://github.com/OriginVorfeed/smartdns-china-list)

- Xray 规则：[xray-china-list](https://github.com/OriginVorfeed/xray-china-list)

- Shadowrocket 规则：[shadowrocket-china-list](https://github.com/OriginVorfeed/shadowrocket-china-list)

## 规则说明

参照 dnsmasq-china-list 中 [Makefile](https://github.com/felixonmars/dnsmasq-china-list/blob/master/Makefile) 的逻辑，转换为对应的 **sing-box 白名单规则**。

具体转换逻辑，请查看 [workflow](https://github.com/OriginVorfeed/singbox-china-list/blob/main/.github/workflows/update.yml)。

可以在 [data 目录](https://github.com/OriginVorfeed/singbox-china-list/tree/main/data) 查看编译前的源文件。

每套规则提供2个链接，第1个需要代理才能稳定访问，第2个可以直接访问，但会延迟12小时。

- **geosite-cn.srs**：

  主规则，包含10w多个适合直连的域名。二进制规则集的匹配时间一般都在微秒级，和毫秒级的网络延时相比，可以忽略不计。
  - [https://raw.githubusercontent.com/OriginVorfeed/singbox-china-list/master/geosite-cn.srs](https://raw.githubusercontent.com/OriginVorfeed/singbox-china-list/master/geosite-cn.srs)
  - [https://cdn.jsdelivr.net/gh/OriginVorfeed/singbox-china-list@master/geosite-cn.srs](https://cdn.jsdelivr.net/gh/OriginVorfeed/singbox-china-list@master/geosite-cn.srs)

- **geosite-private.srs**：

  一份精简过的私有域名列表，不包含 `内网 DNS 反查、各品牌路由器后台地址、软件内部通信域名` 等不太常用的内容。
  - [https://raw.githubusercontent.com/OriginVorfeed/singbox-china-list/master/geosite-private.srs](https://raw.githubusercontent.com/OriginVorfeed/singbox-china-list/master/geosite-private.srs)
  - [https://cdn.jsdelivr.net/gh/OriginVorfeed/singbox-china-list@master/geosite-private.srs](https://cdn.jsdelivr.net/gh/OriginVorfeed/singbox-china-list@master/geosite-private.srs)

- **geosite-apple.srs**：

  可选规则，推荐使用。Apple 相关域名在国内有 CDN 加速，理论上适合直连。但如果你发现解析到了国外，就不要使用。
  - [https://raw.githubusercontent.com/OriginVorfeed/singbox-china-list/master/geosite-apple.srs](https://raw.githubusercontent.com/OriginVorfeed/singbox-china-list/master/geosite-apple.srs)
  - [https://cdn.jsdelivr.net/gh/OriginVorfeed/singbox-china-list@master/geosite-apple.srs](https://cdn.jsdelivr.net/gh/OriginVorfeed/singbox-china-list@master/geosite-apple.srs)

- **geosite-google.srs**：

  可选规则，不推荐使用。你要是发现熟悉的网页上，一些图标突然变成了文字，就是直连 fonts.gstatic.com 不稳定导致的。
  - [https://raw.githubusercontent.com/OriginVorfeed/singbox-china-list/master/geosite-google.srs](https://raw.githubusercontent.com/OriginVorfeed/singbox-china-list/master/geosite-google.srs)
  - [https://cdn.jsdelivr.net/gh/OriginVorfeed/singbox-china-list@master/geosite-google.srs](https://cdn.jsdelivr.net/gh/OriginVorfeed/singbox-china-list@master/geosite-google.srs)

## 使用方法

- 推荐配合 [v2rayN](https://github.com/2dust/v2rayn) 使用，填写 `设置 -> 参数设置 -> v2rayN 设置 -> sing-box ruleset 文件来源`，任选其一：

  ```
  # 需要代理
  https://raw.githubusercontent.com/OriginVorfeed/singbox-china-list/refs/heads/main/{1}.srs

  # 可以直连，但最好别用。
  # 试了好几次，v2rayN 下载到的文件大小不对，但浏览器下载是好的，我也不知道为什么跌丝袜。
  https://cdn.jsdelivr.net/gh/OriginVorfeed/singbox-china-list@main/{1}.srs
  ```

- `帮助 -> 检查更新`，勾选 GeoFiles，点击 `检查更新`。
- 文件名已匹配预置的 `绕过大陆(Whitelist)` 规则集，可以直接 `设为活动规则`。

> 单独配置时，在 `rule-set` 里指定 `path`，即可和其他 sing-box srs 文件配合使用。
>
> 请参考 [sing-box 官方文档](https://sing-box.sagernet.org/zh/configuration/route/)，合并以下内容：

```json
{
  "route": {
    "rules": [
      {
        "outbound": "direct",
        "rule_set": [
          "singbox-china-list-private",
          "singbox-china-list-cn",
          "singbox-china-list-apple"
        ]
      },
      {
        "outbound": "direct",
        "rule_set": [
          "geoip-cn"
        ]
      }
    ],
    "rule_set": [
      {
        "tag": "singbox-china-list-private",
        "type": "local",
        "format": "binary",
        "path": "C:\\srss\\geosite-private.srs"
      },
      {
        "tag": "singbox-china-list-cn",
        "type": "local",
        "format": "binary",
        "path": "C:\\srss\\geosite-cn.srs"
      },
      {
        "tag": "singbox-china-list-apple",
        "type": "local",
        "format": "binary",
        "path": "C:\\srss\\geosite-apple.srs"
      },
      {
        "tag": "geoip-cn",
        "type": "local",
        "format": "binary",
        "path": "C:\\srss\\geoip-cn.srs"
      }
    ]
  }
}
```

## 验证配置

 - 在 v2rayN 里 `启用 Tun`。

 - 访问 [https://ip111.cn/](https://ip111.cn/)。
 - `从国内测试、从国外测试` 应该都是你的本地 IP，`从谷歌测试` 应该是你的代理 IP。

## 常见问题

- **如何恢复 v2rayN 默认的 sing-box ruleset？**

  清空 `设置 -> 参数设置 -> v2rayN 设置 -> sing-box ruleset 文件来源` 后，再次更新 GeoFiles 即可。

- **可以不覆盖 v2rayN 预置的规则文件吗？**

  可以，但不推荐，无论如何都会造成 sing-box、Xray 分流行为不一致。如果你不介意这点，配置方法如下：

  - 新建一个 json 文件，比如你想指定 `geosite:cn` 对应的 srs 文件，就填写：

    ```json
    [
      {
        "tag": "geosite-cn",
        "type": "local",
        "format": "binary",
        "path": "C:\\srss\\custom-geosite-cn.srs"
      }
    ]
    ```

  - `设置 -> 路由设置 -> 规则集设置 -> 自定义 sing-box rule-set`，选择这个 json 文件。
  - 应用设置后，v2rayN 生成的 sing-box 配置文件里，`rule_set -> tag: geosite-cn` 的内容就会被 json 替换。

    > 但此时，Xray 依然使用预置的 geosite.dat，导致两者分流行为不一致。

## 问题反馈

任何问题欢迎在 [Issues](https://github.com/OriginVorfeed/singbox-china-list/issues) 中反馈。
