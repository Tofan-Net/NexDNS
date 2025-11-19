# NexDNS — Enterprise DNS Filtering & Control System
High-performance DNS filtering, security enforcement, and game-blocking system built using **Pi-hole** and **MikroTik** infrastructure.  
Designed and deployed by **Tofan Net ICT & Consulting Company**, Herat, Afghanistan.

## 📌 Overview
**NexDNS** provides secure, controlled, and policy-driven DNS filtering for internal services and customer-facing platforms.  
This setup is optimized for:
- High-traffic ISP environments  
- Game/application blocking  
- Controlled access policies  
- DNS-only access for approved servers  
- Logging & performance stability  
- Prevention of DNS flooding and retry loops  

## 🔧 Architecture Summary
### Core Components
- Pi-hole (FTL + DNSMasq)
- Ubuntu LTS
- MikroTik CCR / RouterOS 7.x
- Tofan Net internal monitoring

### Flow Diagram
```
[ Internet Users ] → (Blocked)
                               \
                                [ MikroTik Firewall ]
                                         ↓
                              [ Allowed Web Servers ]
                                         ↓  
                                   [ NexDNS / Pi-hole ]
                                         ↓
                                 [ Root DNS Servers ]
```

## 🚨 Security Model
NexDNS operates using a Deny-By-Default access model.

### 1. Pi-hole accepts DNS queries ONLY from approved hosts
Set:
```
Permit only the following networks to use this DNS server
```

### 2. Firewall is the first line of defense
```
/ip firewall filter
add chain=input protocol=udp dst-port=53 action=drop
add chain=input protocol=tcp dst-port=53 action=drop
add chain=input protocol=udp dst-port=53 src-address=YOUR_SERVER_IP action=accept
add chain=input protocol=tcp dst-port=53 src-address=YOUR_SERVER_IP action=accept
```

## 🛡 DNS Loop Protection & Whitelisting Logic
Safe whitelist:
```
asia.pool.ntp.org
connectivitycheck.unisoc.com
resolv.msg.global.xiaomi.net
connectivitycheck.platform.hihonorcloud.com
jupiter.intl.sys.miui.com
app.chat.global.xiaomi.net
api.brs.intl.miui.com
connect.rom.miui.com
api.gallery.intl.miui.com
tracking.intl.miui.com
mcc.intl.inf.miui.com
api.ad.intl.xiaomi.com
sdkconfig.ad.intl.xiaomi.com
```

## ❌ PUBG-Mobile Blocking
```
igamecj.com
ig-us-sdkapi-cf.com
awsdns-cn-portal.com
igamecj.net
tencent-cloud.net
cdn.igamecj.com
```

## 📂 Repository Structure
```
/config
/firewall
/docs
/scripts
README.md
```

## 📊 Monitoring
```
pihole -t
pihole -g
pihole status
```

## 👨‍💼 Maintainers
Tofan Net ICT and Consulting Company  
Ferdousi-4, Herat, Afghanistan

## 📜 License
© 2025 Tofan Net ICT and Consulting Company. All rights reserved.
