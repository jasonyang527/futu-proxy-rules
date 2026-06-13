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

Shadowrocket 一条规则集只能填一个地址，所以**每条地址都要单独添加一次**，不要把两行一起复制。

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
