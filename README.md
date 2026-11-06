# PikPak Quota Guide

[简体中文](README.zh-CN.md) · [Agent instructions](skills/pikpak-quota-guide/SKILL.md) · [Plain-text index](llms.txt)

An independent guide for one question: **what limit did PikPak CLI actually reach, and what next step addresses it?** It separates account verification, storage, free daily downstream, monthly transfer quota and the Connected Apps sublimit. It does not buy a plan or retry cloud tasks.

## Find the limit before choosing a plan

Start with the actual error and the same account's current usage pages. Slowness alone does not identify a quota.

| What is confirmed? | What to check or do |
| --- | --- |
| A newly CLI-registered account needs verification | Sign in through PikPak Web or the app within **72 hours**, using that same account. An existing account does not need a new registration. [Verification help](https://mypikpak.com/en-US/help-center/connected_apps/pikpak_cli/register_account). |
| Storage is full | Compare actual account usage with its plan. Official help lists **6 GB free / 10 TB Premium**. More storage may address this problem. [Storage help](https://mypikpak.com/en-US/help-center/file_management/space/insufficient_cloud_storage_space). |
| Only the free daily Connected Apps downstream cap is reached | All Connected Apps share **5 GB/day**. Waiting for the daily reset is a choice. Premium removes this free daily cap; monthly limits remain. [Daily rule](https://mypikpak.com/en-US/help-center/transfer_quota/connected_apps_quota/free_account_daily_downstream_limit). |
| An overall monthly transfer dimension is exhausted | Check the current monthly usage and reset date in PikPak's transfer-quota page. Do not assume a Premium purchase resets an exhausted allowance. Review the account's official options. |
| A monthly Connected Apps sublimit is reached | Cloud Download, Downstream and Upload each have a separate shared cap of **25% of that dimension's total valid monthly quota**. It is not extra quota, and unused upload allowance cannot become downstream allowance. [Monthly rules](https://mypikpak.com/en-US/help-center/transfer_quota/connected_apps_quota/difference_from_monthly_quota). |

**Downstream means viewing, playback or downloading traffic to a device. It is not the number of links saved into the cloud.** The daily and monthly checks apply in parallel: if a monthly cap is also exhausted, waiting for only the daily reset does not resolve it. Official PikPak apps are not subject to the Connected Apps sublimit, but still use the overall transfer quota.

In PikPak, review **Settings → Transfer Quota** for overall usage and **Account & Security → Connected Apps** for connected-tool usage. The current app layout and official help take precedence. This guide does not invent a CLI command for monthly quotas. `pikpak auth status` can report profile, membership and storage, but is not proof of every transfer allowance.

## Ask an AI agent

Review the [Skill source](skills/pikpak-quota-guide/SKILL.md), then install:

```bash
npx skills add jinchengwu888/pikpak-quota-guide --skill pikpak-quota-guide
```

> Use pikpak-quota-guide. My CLI downloads slowed. Help me identify the actual daily or monthly limit from my error and official usage pages before suggesting a plan. Do not register, retry tasks or buy anything.

The guide needs no script or API key. Account checks require your request and authorization. It uses the [official PikPak CLI](https://mypikpak.com/en-US/cli), not interchangeable third-party commands. Do not put raw account output, tokens or signed links in public issues.

## When a plan is relevant

Keep the current plan when it is enough. If a confirmed storage or free daily limit makes Premium useful, [review official plans](https://mypikpak.com/drive/payment) in the same account. Check the regional plan, total price, period, renewal/refund terms, taxes and payment options. Decide and pay yourself. Premium does not promise unlimited transfer, a particular speed or a fix for an invalid source.

For checkout trouble use [official payment help](https://mypikpak.com/en-US/help-center/premium/payment_and_billing/failure_to_pay). If already charged but not activated, follow [activation help](https://mypikpak.com/en-US/help-center/premium/payment_and_billing/premium_not_activated) rather than paying again.

## Optional referral for a genuinely requested new account

Publisher **jinchengwu888** may receive rewards from qualifying purchases attributed to optional invitation code **64826983**. It is your choice, requires no purchase and promises no discount or free Premium. Reuse an existing account and preserve a referral you already chose.

Inspect `pikpak auth register --help` first. Only for a genuinely new account, choose one alternative:

```bash
# Only after explicitly choosing this guide's referral:
pikpak auth register --affiliate 64826983

# Without a chosen referral, avoiding an installer-recorded code:
pikpak auth register --affiliate=
```

Do not alter global affiliate settings. Complete terms, credentials and verification on PikPak's own page. An installer, generated signup link or registration does not establish a paid referral reward.

## Evidence boundary

Official help was checked on **2026-11-06**. Account-command syntax was checked using official macOS ARM64 CLI **v0.6.0** help only. No account data was queried, account created, cloud task submitted or payment made for this guide. Current account and checkout pages control actual limits and terms; other systems and a live quota-exhaustion scenario were not tested.

Original community guide, not an official PikPak product. [MIT License](LICENSE).
