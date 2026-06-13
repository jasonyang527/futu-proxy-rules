# futu-proxy-rules

富途域名分流规则

## 使用方法

### Shadowrocket

#### 方法一：在 App 里手动添加（推荐新手）

1. 打开 Shadowrocket，点底部「配置」标签。
2. 找到当前正在使用的配置（名字后面有勾的那个），点它右边的蓝色 ⓘ(i) 按钮。
3. 进去后选「规则」(Rule)。
4. 点右上角或底部的「+ / 添加规则」。
5. 类型选「RULE-SET（规则集）」，把地址粘进去，行为(Action) 选「PROXY（代理）」。

两个都要加：

核心列表：

```text
https://raw.githubusercontent.com/jasonyang527/futu-proxy-rules/main/Futu.list
```

扩展列表：

```text
https://raw.githubusercontent.com/jasonyang527/futu-proxy-rules/main/Futu_Extended.list
```

> 行为这里要选「PROXY（代理）」，不要选 DIRECT，否则富途流量仍然走直连、连不上。

#### 方法二：直接改配置文件

在 Shadowrocket 配置的 `[Rule]` 段里加入以下规则：

```ini
[Rule]
RULE-SET,https://raw.githubusercontent.com/jasonyang527/futu-proxy-rules/main/Futu.list,PROXY
FINAL,DIRECT
```

如果还要启用扩展规则集：

```ini
[Rule]
RULE-SET,https://raw.githubusercontent.com/jasonyang527/futu-proxy-rules/main/Futu.list,PROXY
RULE-SET,https://raw.githubusercontent.com/jasonyang527/futu-proxy-rules/main/Futu_Extended.list,PROXY
FINAL,DIRECT
```

注意把这些规则放在最终兜底规则（比如 `FINAL,DIRECT`）之前。

### Surge

在 Surge 配置的 `[Rule]` 段里加入以下规则：

```ini
[Rule]
RULE-SET,https://raw.githubusercontent.com/jasonyang527/futu-proxy-rules/main/Futu.list,PROXY
FINAL,DIRECT
```

如果还要启用扩展规则集：

```ini
[Rule]
RULE-SET,https://raw.githubusercontent.com/jasonyang527/futu-proxy-rules/main/Futu.list,PROXY
RULE-SET,https://raw.githubusercontent.com/jasonyang527/futu-proxy-rules/main/Futu_Extended.list,PROXY
FINAL,DIRECT
```

这里的 `PROXY` 是你的代理策略名。如果你的策略组叫别的名字（比如 `Proxy`、`节点选择`），把 `PROXY` 换成你自己的策略名即可。

### sing-box

sing-box 跟 Shadowrocket / Surge 不一样，**不能远程引用本仓库的 `.list` 文件**。sing-box 的 `rule_set` 只认 `.srs` 二进制或 sing-box 自己的 JSON 源格式，认不了 Surge 那种纯文本 `.list`。所以富途规则要**直接内联**写进配置的 `route.rules` 里。

把下面两条规则加到你配置 `route.rules` 数组的**最前面**（放在国内直连、`geoip-cn` 之类的兜底规则之前，否则富途的国内 IP 会被国内规则抢先匹配走直连），并把 `outbound` 换成你自己的代理出站 tag（比如你的 selector 名字）：

```json
{
  "domain_suffix": [
    "futu.link",
    "futu.com",
    "futu.cn",
    "futunn.com",
    "futu0.com",
    "futu1.com",
    "futu2.com",
    "futu3.com",
    "futu4.com",
    "futu5.com",
    "futu6.com",
    "futu7.com",
    "futu8.com",
    "futu9.com",
    "futuau.com",
    "futuesop.com",
    "futufin.com",
    "futuhk.com",
    "futuhk2.com",
    "futuhkapp.com",
    "futuhn.com",
    "futuholdings.com",
    "futuinc.com",
    "futuniuniu.com",
    "futubull.cn",
    "futuchain.com",
    "futustatic.com",
    "fututrade.com",
    "fututrustee.com",
    "moomoo.com",
    "moomoobull.com",
    "moomooequity.com",
    "moomootrustee.com",
    "9oju31.launches.appsflyersdk.com",
    "sgqt0j.launches.appsflyersdk.com",
    "shortconn.im.qcloud.com"
  ],
  "outbound": "YOUR_PROXY"
},
{
  "ip_cidr": [
    "1.14.242.0/23",
    "14.152.91.0/24",
    "38.65.217.0/24",
    "42.193.128.0/24",
    "43.130.30.0/24",
    "43.130.170.0/24",
    "43.132.107.0/24",
    "43.135.64.0/24",
    "43.135.82.0/24",
    "43.142.232.0/24",
    "43.145.30.0/24",
    "43.153.191.0/24",
    "43.153.233.0/24",
    "43.160.156.0/24",
    "49.51.78.0/24",
    "49.234.241.0/24",
    "101.32.198.0/24",
    "106.55.66.0/23",
    "111.230.119.0/24",
    "111.230.214.0/24",
    "119.28.37.0/24",
    "119.28.141.0/24",
    "119.28.183.0/24",
    "119.29.48.0/23",
    "119.91.245.0/23",
    "119.147.110.0/24",
    "121.5.97.0/24",
    "124.156.124.0/24",
    "124.156.233.0/24",
    "124.156.234.0/24",
    "129.226.79.0/24",
    "129.226.111.0/24",
    "162.14.10.0/24",
    "170.106.48.0/23",
    "170.106.62.0/24",
    "183.60.225.0/24",
    "193.112.84.0/24",
    "193.112.234.0/24",
    "170.106.201.0/24",
    "175.178.207.0/24",
    "43.134.158.106/32",
    "43.132.138.6/32",
    "119.28.201.30/32",
    "49.51.77.113/32",
    "43.153.234.107/32",
    "43.153.249.33/32",
    "43.163.17.229/32",
    "42.194.152.250/32",
    "43.132.106.6/32",
    "43.132.106.8/32",
    "43.132.138.67/32",
    "1.15.158.235/32"
  ],
  "outbound": "YOUR_PROXY"
}
```

> 为什么拆成两条？sing-box 同一条规则里不同字段是「与」关系，`domain_suffix` 和 `ip_cidr` 写在一起会要求同时满足，永远匹配不上，所以域名和 IP 必须分开写。

## 规则文件格式

规则文件是标准的 rule-set 文件。

每行只包含规则本身，不带 `DIRECT`、`PROXY` 之类的策略名。

示例：

```ini
DOMAIN-SUFFIX,moomoo.com
DOMAIN-SUFFIX,futunn.com
IP-CIDR,1.14.242.0/23,no-resolve
```

策略名是在引用规则集时指定的：

```ini
RULE-SET,https://raw.githubusercontent.com/jasonyang527/futu-proxy-rules/main/Futu.list,PROXY
```

## 许可证

MIT
