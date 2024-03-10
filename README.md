## Potplayer

一般用于禁止potplayer检查更新和拉取广告

rule-providers配置:

```yaml
rule-providers:
  potplayer:
    type: http
    behavior: classical
    format: yaml
    url: "https://mirror.ghproxy.com/https://github.com/HaibaAi/ClashProfileFix/blob/main/potplayer.yaml"
    path: ./ruleset/potplayer.yaml
    interval: 86400
```

## directFix

修复直连规则不完善的配置

包括:

- 微信.exe
- 游戏需要直连的域名

rule-providers配置:

```yaml
rule-providers:
  directFix:
    type: http
    behavior: classical
    format: yaml
    url: "https://mirror.ghproxy.com/https://github.com/HaibaAi/ClashProfileFix/blob/main/directFix.yaml"
    path: ./ruleset/directFix.yaml
    interval: 86400
```

## dashboard

clash webui的配置面板域名,一般用于直连

他们的dns解析地址一般是

> 2606:50c0:8001::153
> 
> 2606:50c0:8002::153
>
> 2606:50c0:8003::153
>
> 2606:50c0:8000::153
>
> 185.199.111.153
>
> 185.199.109.153
>
> 185.199.108.153
>
> 185.199.110.153

rule-providers配置:

```yaml
rule-providers:
  dashboard:
    type: http
    behavior: classical
    format: yaml
    url: "https://mirror.ghproxy.com/https://github.com/HaibaAi/ClashProfileFix/blob/main/dashboard.yaml"
    path: ./ruleset/dashboard.yaml
    interval: 86400
```

## proxyFix

修复代理规则不完善的配置

rule-providers配置:

```yaml
rule-providers:
  proxyFix:
    type: http
    behavior: classical
    format: yaml
    url: "https://mirror.ghproxy.com/https://github.com/HaibaAi/ClashProfileFix/blob/main/proxyFix.yaml"
    path: ./ruleset/proxyFix.yaml
    interval: 86400
```

## 最终配置-搭配clash rule

```yaml
proxy-groups:
  - name: Proxy
    type: select
    proxies:
    
  - name: Apple and Icloud
    type: select
    proxies:
      - DIRECT
      - Proxy

  - name: PotplayerRule
    type: select
    proxies:
      - REJECT
      - Proxy

  - name: Others
    type: select
    proxies:
      - DIRECT
      - Proxy
rule-providers:

  reject:
    type: http
    behavior: domain
    url: "https://mirror.ghproxy.com/https://raw.githubusercontent.com/Loyalsoldier/clash-rules/release/reject.txt"
    path: ./ruleset/reject.yaml
    interval: 86400
  
  icloud:
    type: http
    behavior: domain
    url: "https://mirror.ghproxy.com/https://raw.githubusercontent.com/Loyalsoldier/clash-rules/release/icloud.txt"
    path: ./ruleset/icloud.yaml
    interval: 86400

  apple:
    type: http
    behavior: domain
    url: "https://mirror.ghproxy.com/https://raw.githubusercontent.com/Loyalsoldier/clash-rules/release/apple.txt"
    path: ./ruleset/apple.yaml
    interval: 86400

  proxy:
    type: http
    behavior: domain
    url: "https://mirror.ghproxy.com/https://raw.githubusercontent.com/Loyalsoldier/clash-rules/release/proxy.txt"
    path: ./ruleset/proxy.yaml
    interval: 86400

  direct:
    type: http
    behavior: domain
    url: "https://mirror.ghproxy.com/https://raw.githubusercontent.com/Loyalsoldier/clash-rules/release/direct.txt"
    path: ./ruleset/direct.yaml
    interval: 86400

  private:
    type: http
    behavior: domain
    url: "https://mirror.ghproxy.com/https://raw.githubusercontent.com/Loyalsoldier/clash-rules/release/private.txt"
    path: ./ruleset/private.yaml
    interval: 86400

  telegramcidr:
    type: http
    behavior: ipcidr
    url: "https://mirror.ghproxy.com/https://raw.githubusercontent.com/Loyalsoldier/clash-rules/release/telegramcidr.txt"
    path: ./ruleset/telegramcidr.yaml
    interval: 86400

  cncidr:
    type: http
    behavior: ipcidr
    url: "https://mirror.ghproxy.com/https://raw.githubusercontent.com/Loyalsoldier/clash-rules/release/cncidr.txt"
    path: ./ruleset/cncidr.yaml
    interval: 86400

  lancidr:
    type: http
    behavior: ipcidr
    url: "https://mirror.ghproxy.com/https://raw.githubusercontent.com/Loyalsoldier/clash-rules/release/lancidr.txt"
    path: ./ruleset/lancidr.yaml
    interval: 86400

  applications:
    type: http
    behavior: classical
    url: "https://mirror.ghproxy.com/https://raw.githubusercontent.com/Loyalsoldier/clash-rules/release/applications.txt"
    path: ./ruleset/applications.yaml
    interval: 86400

  potplayer:
    type: http
    behavior: classical
    format: yaml
    url: "https://mirror.ghproxy.com/https://github.com/HaibaAi/ClashProfileFix/blob/main/potplayer.yaml"
    path: ./ruleset/potplayer.yaml
    interval: 86400

  dashboard:
    type: http
    behavior: classical
    format: yaml
    url: "https://mirror.ghproxy.com/https://github.com/HaibaAi/ClashProfileFix/blob/main/dashboard.yaml"
    path: ./ruleset/dashboard.yaml
    interval: 86400  

  directFix:
    type: http
    behavior: classical
    format: yaml
    url: "https://mirror.ghproxy.com/https://github.com/HaibaAi/ClashProfileFix/blob/main/directFix.yaml"
    path: ./ruleset/directFix.yaml
    interval: 86400

  proxyFix:
    type: http
    behavior: classical
    format: yaml
    url: "https://mirror.ghproxy.com/https://github.com/HaibaAi/ClashProfileFix/blob/main/proxyFix.yaml"
    path: ./ruleset/proxyFix.yaml
    interval: 86400
    
rules:

  # 去广告
  - RULE-SET,reject,REJECT
  # 内网地址
  - RULE-SET,private,DIRECT
  - RULE-SET,lancidr,DIRECT,no-resolve
  # 需要直连的常见软件列表 applications.txt
  - RULE-SET,applications,DIRECT

  # 自定义:
  # dashboard
  - RULE-SET,dashboard,DIRECT
  # apple and icloud
  - RULE-SET,apple,Apple and Icloud
  - RULE-SET,icloud,Apple and Icloud
  # telegram
  - RULE-SET,telegramcidr,Proxy
  # potplayer
  - RULE-SET,potplayer,PotplayerRule
  # proxy_fix:
  - RULE-SET,proxyFix,Proxy
  # direct_fix:
  - RULE-SET,directFix,DIRECT
  
  # 总则
  - RULE-SET,proxy,Proxy
  - RULE-SET,direct,DIRECT
  - RULE-SET,cncidr,DIRECT

  # 未匹配部分
  - MATCH,Others
```
## 常见局域网保留ip

\<local\> 只测试了windows,未测试linux下的情况

```txt
localhost;127.*;10.*;172.16.*;172.17.*;172.18.*;172.19.*;172.20.*;172.21.*;172.22.*;172.23.*;172.24.*;172.25.*;172.26.*;172.27.*;172.28.*;172.29.*;172.30.*;172.31.*;192.168.*;*.edu.cn;<local>
```


