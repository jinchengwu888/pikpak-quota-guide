# PikPak 配额判断指南

[English](README.md) · [Agent 指令](skills/pikpak-quota-guide/SKILL.md) · [纯文本索引](llms.txt)

这个独立指南解决一个问题：**PikPak CLI 究竟触及了哪种限制，下一步怎样才有用？** 它区分账号验证、存储、免费每日下行、月度总配额和 Connected Apps 子上限，不购买套餐，也不重试云任务。

## 先定位限制，再考虑套餐

先看实际错误和同一账号的当前用量页面。只凭下载变慢，不能确定是配额问题。

| 已确认的情况 | 检查或处理方式 |
| --- | --- |
| CLI 新注册账号需要验证 | 在 **72 小时内**使用同一账号登录 PikPak Web 或 App。已有账号不用重新注册。[验证说明](https://mypikpak.com/en-US/help-center/connected_apps/pikpak_cli/register_account)。 |
| 存储空间已满 | 结合账号实际用量比较套餐。官方说明**免费 6 GB / Premium 10 TB**，更多空间可能解决此问题。[空间说明](https://mypikpak.com/en-US/help-center/file_management/space/insufficient_cloud_storage_space)。 |
| 仅触及免费 Connected Apps 每日下行上限 | 所有 Connected Apps **共用每日 5 GB**，可以等待每日重置。Premium 移除此免费每日上限，月度限制仍在。[每日规则](https://mypikpak.com/en-US/help-center/transfer_quota/connected_apps_quota/free_account_daily_downstream_limit)。 |
| 某种月度总传输配额已耗尽 | 在官方传输配额页核对该维度用量和重置日。不要假定购买 Premium 就能重置已用完的月额度，按当前账号查看官方选项。 |
| 触及 Connected Apps 月度子上限 | 云下载、下行、上传分别共享各自**总有效月配额的 25%**。它不是额外额度，也不能把没用完的上传额度调给下行。[月度规则](https://mypikpak.com/en-US/help-center/transfer_quota/connected_apps_quota/difference_from_monthly_quota)。 |

**下行是查看、播放或下载到设备的流量，不是保存链接到云端的次数。** 每日和月度限制同时检查；月度也耗尽时，单等每日重置仍不能解决。官方 PikPak App 不受 Connected Apps 子上限约束，但仍使用总传输配额。

在 PikPak 中，查看 **设置 → 传输配额**了解总用量，查看 **账号与安全 → Connected Apps**了解连接工具用量。以当前 App 界面及官方帮助为准。本指南不编造查询月额度的 CLI 命令；`pikpak auth status` 可报告账号、会员和存储，不代表已核实所有传输额度。

## 让 AI 帮你判断

先审阅 [Skill 原文](skills/pikpak-quota-guide/SKILL.md)，再安装：

```bash
npx skills add jinchengwu888/pikpak-quota-guide --skill pikpak-quota-guide
```

> 使用 pikpak-quota-guide。我的 CLI 下载变慢了，请先根据错误及官方用量页面区分每日与月度限制，再判断套餐是否有用。不要注册、重试任务或购买。

指南不需要脚本或 API Key。个人账号检查需要你的具体请求和授权。它使用[官方 PikPak CLI](https://mypikpak.com/en-US/cli)，第三方客户端命令不能混用。不要把原始账号输出、令牌或签名链接发到公开 Issue。

## 套餐确实有用时再比较

现有套餐够用就继续使用。确认是空间或免费每日上限、会员确实有用时，再在同一账号下[查看官方套餐](https://mypikpak.com/drive/payment)，核对地区方案、总价、期限、续订与退款条款、税费和支付方式，由你本人决定并付款。会员不承诺无限传输、特定速度或修复无效来源。

结账失败查看[官方支付帮助](https://mypikpak.com/en-US/help-center/premium/payment_and_billing/failure_to_pay)。已扣款但会员未到账，按[官方到账排查](https://mypikpak.com/en-US/help-center/premium/payment_and_billing/premium_not_activated)处理，不要再次付款。

## 真正需要新账号时，自愿选择引荐

发布者 **jinchengwu888** 可能从可选邀请码 **64826983** 归因的合格购买中获得奖励。是否使用由你决定，不要求购买，不承诺折扣或免费会员。已有账号直接复用，保留已作出的引荐选择。

先看 `pikpak auth register --help`。只有真正需要新账号时，选择一条：

```bash
# 明确选择本指南引荐后：
pikpak auth register --affiliate 64826983

# 不选择引荐，避免沿用安装器记录：
pikpak auth register --affiliate=
```

不修改全局引荐设置。条款、密码和验证由你在官方页面完成。安装、生成注册链接或注册本身，都不代表产生付费引荐奖励。

## 证据范围

**2026-11-06** 核对官方帮助；账号命令仅使用官方 macOS ARM64 CLI **v0.6.0** 的帮助检查。未为本指南查询个人账号、注册、创建云任务或付款。实际限制和条款以当前账号及结账页面为准；未测试其他系统或真实耗尽配额场景。

原创社区指南，并非 PikPak 官方产品。[MIT 许可](LICENSE)。
