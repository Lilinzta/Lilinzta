# clash-verge-rev-merge

自用 clash-verge-rev 全局扩展配置

```yaml
profile:
  store-selected: true
proxy-providers-common: &ppc
  type: http
  interval: 86400
proxy-groups-common: &pgc
  type: select
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
proxy-providers:
  sub1:
    <<: *ppc
    url:
    path: ./proxy-provider/sub1.yaml
  sub2:
    <<: *ppc
    url:
    path: ./proxy-provider/sub2.yaml
  sub3:
    <<: *ppc
    url:
    path: ./proxy-provider/sub3.yaml
  sub4:
    <<: *ppc
    url:
    path: ./proxy-provider/sub4.yaml
proxy-groups:
  - name: miHoYo
    <<: *pgc
    proxies:
      - Honkai Impact 3rd
      - Genshin Impact
      - "Honkai: Star Rail"
      - Zenless Zero Zone
    icon: https://fastcdn.mihoyo.com/mi18n/plat_cn/m202004281054311/upload/fb9fb8e171957fc3a06322e5f19c772f_6978451248621653135.png
  - name: Honkai Impact 3rd
    <<: *pgc
    use:
      - sub1
    icon: https://webstatic.mihoyo.com/upload/op-public/2021/10/11/bcfac93531d35c27fd2c44fbc83cfd68_2546351942566697749.png
  - name: Genshin Impact
    <<: *pgc
    use:
      - sub2
    icon: https://webstatic.mihoyo.com/upload/op-public/2021/10/09/def1f2abcfc2af0bbe2e5900a60a5ee1_178756228418778568.png
  - name: "Honkai: Star Rail"
    <<: *pgc
    use:
      - sub3
    icon: https://webstatic.mihoyo.com/upload/op-public/2021/10/09/870472d6104dbbe7ea18b27c13763ccb_3190195711986871508.png
  - name: Zenless Zero Zone
    <<: *pgc
    use:
      - sub4
    icon: https://webstatic.mihoyo.com/upload/op-public/2022/07/12/3896559583929f643fbe39ec1d6ca1c9_5788444135694206615.png
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
  - RULE-SET,reject,REJECT
  - DOMAIN-SUFFIX,girigirilove.com,DIRECT
  - DOMAIN-SUFFIX,netlify.app,DIRECT
  - DOMAIN,openrouter.ai,DIRECT
  - RULE-SET,applications,DIRECT
  - RULE-SET,private,DIRECT
  - RULE-SET,icloud,DIRECT
  - RULE-SET,apple,DIRECT
  - RULE-SET,direct,DIRECT
  - RULE-SET,lancidr,DIRECT
  - RULE-SET,cncidr,DIRECT
  - GEOIP,LAN,DIRECT
  - GEOIP,CN,DIRECT
  - RULE-SET,telegramcidr,miHoYo
  - RULE-SET,google,miHoYo
  - RULE-SET,proxy,miHoYo
  - MATCH,miHoYo
```
