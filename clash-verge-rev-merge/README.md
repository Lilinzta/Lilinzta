# clash-verge-rev-merge

自用 clash-verge-rev 全局扩展配置

```yaml
profile:
  store-selected: true
domesticNameservers: &dn
  - https://dns.alidns.com/dns-query
  - https://doh.pub/dns-query
  - https://doh.360.cn/dns-query
foreignNameservers: &fn
  - https://1.1.1.1/dns-query
  - https://1.0.0.1/dns-query
  - https://208.67.222.222/dns-query
  - https://208.67.220.220/dns-query
  - https://194.242.2.2/dns-query
  - https://194.242.2.3/dns-query
proxy-providers-common: &ppc
  type: http
  interval: 86400
proxy-groups-common: &pgc
  interval: 300
  timeout: 3000
  url: https://www.google.com/generate_204
  lazy: true
  max-failed-times: 3
  hidden: false
rule-providers-common: &rpc
  type: http
  format: yaml
  interval: 86400
dns:
  enable: true
  listen: 0.0.0.0:1053
  ipv6: true
  cache-algorithm: arc
  enhanced-mode: fake-ip
  fake-ip-range: 198.18.0.1/16
  fake-ip-filter:
    - +.lan
    - +.local
    - +.msftconnecttest.com
    - +.msftncsi.com
    - localhost.ptlogin2.qq.com
    - localhost.sec.qq.com
    - localhost.work.weixin.qq.com
  default-nameserver:
    - 223.5.5.5
    - 119.29.29.29
    - 1.1.1.1
    - 8.8.8.8
  nameserver:
    - *dn
    - *fn
  proxy-server-nameserver:
    - *dn
    - *fn
  nameserver-policy:
    geosite:private,cn,geolocation-cn: *dn
    geosite:google,youtube,telegram,gfw,geolocation-!cn: *fn
proxy-providers:
  pp1:
    <<: *ppc
    url: https://example.com
    path: ./proxy-provider/pp1.yaml
  pp2:
    <<: *ppc
    url: https://example.com
    path: ./proxy-provider/pp2.json
  pp3:
    <<: *ppc
    url: https://example.com
    path: ./proxy-provider/pp3.yaml
proxy-groups:
  - name: Selector
    type: select
    <<: *pgc
    proxies:
      - sub1
      - sub2
      - sub3
    icon: https://example.com/example.png
  - name: sub1
    type: select
    <<: *pgc
    use:
      - pp1
    icon: https://example.com/example.png
  - name: sub2
    type: select
    <<: *pgc
    use:
      - pp2
    icon: https://example.com/example.png
  - name: sub3
    type: select
    <<: *pgc
    use:
      - pp3
    icon: https://example.com/example.png
rule-providers:
  reject:
    <<: *rpc
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/reject.txt"
    path: ./ruleset/reject.yaml
  icloud:
    <<: *rpc
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/icloud.txt"
    path: ./ruleset/icloud.yaml
  apple:
    <<: *rpc
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/apple.txt"
    path: ./ruleset/apple.yaml
  google:
    <<: *rpc
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/google.txt"
    path: ./ruleset/google.yaml
  proxy:
    <<: *rpc
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/proxy.txt"
    path: ./ruleset/proxy.yaml
  direct:
    <<: *rpc
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/direct.txt"
    path: ./ruleset/direct.yaml
  private:
    <<: *rpc
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/private.txt"
    path: ./ruleset/private.yaml
  gfw:
    <<: *rpc
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/gfw.txt"
    path: ./ruleset/gfw.yaml
  tld-not-cn:
    <<: *rpc
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/tld-not-cn.txt"
    path: ./ruleset/tld-not-cn.yaml
  telegramcidr:
    <<: *rpc
    behavior: ipcidr
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/telegramcidr.txt"
    path: ./ruleset/telegramcidr.yaml
  cncidr:
    <<: *rpc
    behavior: ipcidr
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/cncidr.txt"
    path: ./ruleset/cncidr.yaml
  lancidr:
    <<: *rpc
    behavior: ipcidr
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/lancidr.txt"
    path: ./ruleset/lancidr.yaml
  applications:
    <<: *rpc
    behavior: classical
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/applications.txt"
    path: ./ruleset/applications.yaml
rules:
  - DOMAIN-SUFFIX,bgm.tv,DIRECT
  - DOMAIN-KEYWORD,spotify,DIRECT
  - DOMAIN-SUFFIX,girigirilove.com,DIRECT
  - DOMAIN-SUFFIX,netlify.app,DIRECT
  - DOMAIN,openrouter.ai,DIRECT
  - RULE-SET,applications,DIRECT
  - RULE-SET,private,DIRECT
  - RULE-SET,icloud,DIRECT
  - RULE-SET,apple,DIRECT
  - RULE-SET,direct,DIRECT
  - RULE-SET,lancidr,DIRECT,no-resolve
  - RULE-SET,cncidr,DIRECT,no-resolve
  - GEOIP,LAN,DIRECT,no-resolve
  - GEOIP,CN,DIRECT,no-resolve
  - RULE-SET,telegramcidr,Selector,no-resolve
  - RULE-SET,google,Selector
  - RULE-SET,proxy,Selector
  - RULE-SET,reject,REJECT
  - MATCH,Selector
```
