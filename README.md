# 美团去广告（Hark）

这是一个面向 Hark/Egern YAML 规则格式的美团去广告模块，当前重点处理美团外卖开屏接口，并过滤少量公开规则中明确标记的广告素材路径。

## 使用方法

在 Egern 的「模块」页面添加以下规则链接并启用：

`https://raw.githubusercontent.com/zhaohaibao19-cmyk/meituan-hark-rules/main/Meituan-hark.yaml`

HTTPS 响应改写需要为列出的域名启用 MITM，并在设备上信任对应证书。若美团 App 出现图片缺失或功能异常，请先停用本模块；个别活动素材可能会复用广告资源路径。

## 规则范围

- 对 `wmapi.meituan.com` 的 `loadInfo` 响应，仅清空已知 JSON 字段 `startpicture.ad` / `startpicture.mk`；遇到未知响应结构时保持原样。
- 对 `openscreen?ad`、`startpicture` 和 `www.meituan.com` 的 `appstatus?ad` 端点使用拒绝字典响应。
- 只拦截公开规则标记的 `adunion`、`display`、`dpmobile`、`midas`、`linglong` 素材路径，以及 `bizad_brandCpt_<数字>.jpg` 这一窄文件名模式；不会屏蔽整个 `img.meituan.net` 或整个 `/bizad/` 目录。
- 不拦截正常推荐接口，也不包含比价功能。规则不保证移除所有信息流或活动广告。

## 验证范围

已在本地验证 YAML 可解析、已知 URL 正则的正向/反向样例，以及 `loadInfo` JSON 改写样例。没有在真实设备或当前美团 App 版本上抓包实测，应用接口变化时可能需要调整。

## 参考来源

- [blackmatrix7 美团广告规则](https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rewrite/Surge/Advertising/Advertising.sgmodule)
- [blackmatrix7 开屏响应脚本](https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/script/startup/startup.js)
- [ihxperfect 美团广告规则](https://raw.githubusercontent.com/ihxperfect/loon-plugin/main/AdBlock.plugin)
- [shui1iao/Fly 美团规则](https://raw.githubusercontent.com/shui1iao/Fly/main/%E5%8E%BB%E5%B9%BF%E5%91%8A.sgmodule)
- [blackmatrix7 issue #762：提醒避免宽泛拦截 bizad 图片目录](https://github.com/blackmatrix7/ios_rule_script/issues/762)
- [Hark 京东规则示例](https://raw.githubusercontent.com/zhaohantao1360-hash/Hark/main/JD-hark.yaml)
