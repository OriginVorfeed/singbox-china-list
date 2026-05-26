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

## 问题反馈

任何问题欢迎在 [Issues](https://github.com/OriginVorfeed/singbox-china-list/issues) 中反馈。
