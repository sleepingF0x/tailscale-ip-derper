# tailscale-ip-derper


## 更新tailscale ACL参数，添加以下内容

https://login.tailscale.com/admin/acls/file

```
	"derpMap": {
		"OmitDefaultRegions": true, // 是否仅使用自定义的 DERP 节点，默认为 false
		"Regions": {
			"900": {
				"RegionID":   900, // 900-999之间
				"RegionCode": "homelab", // 自定义 Code
				"RegionName": "HomeLab", // 自定义名称
				"Nodes": [
					// derp 服务器节点
					{
						"Name":     "HomeLab Server", // 名称
						"RegionID": 900, // 和上面的 regionId 一样
						"HostName": "你的服务器IP", // 域名/IP
						"DERPPort": 19850, // DERP 服务器 HTTPS 端口，默认为 443,用于数据中转
						"STUNPort": 3478, // DERP 服务器 STUN 端口，默认为3478，用于 NAT 穿越的端口
						"InsecureForTests": true,
						"IPv4":             "你的服务器IP",
					},
				],
			},
		},
	},
```

## 

启动 `docker-compose up -d`

尝试访问https://你的服务器IP:derper端口

在tailscale客户端终端上查看运行情况

网络: `tailscale netcheck`

`tailscale status`
没有出现 Health check 字样一般就可以判断成功了


