# notify-on-stop

**Desktop notifications + sound alerts for Claude Code**

---

## The Problem: Your Attention Is a Finite Resource

When you kick off a long task in Claude Code or any AI agent, you face a familiar dilemma: you don't know when it'll finish. So you end up context-switching every few minutes — alt-tabbing back to the terminal, glancing at the screen, then returning to whatever you were doing. Rinse and repeat.

This is costly. If you treat the human brain as an agent of its own, every unnecessary context switch consumes working memory and drains cognitive bandwidth. That idle glance isn't free — it interrupts your flow, breaks your concentration, and accumulates into real fatigue over the course of a day.

There are two better ways to spend that waiting time:

- **Go deep on something else.** With notifications enabled, you can fully commit to another task — writing, reading, a conversation — without reserving any mental capacity to monitor the agent. You get notified the moment it's done or needs your input.

- **Actually rest.** Close your eyes. Meditate. Let your mind recover. This is almost impossible to do when you're half-watching a terminal window and half-scrolling through your phone "just in case." With audio alerts, you can genuinely step away from screens and let your auditory system take the watch — freeing up your cognitive context to actually reset

Compared to purpose-built attention devices like traffic lights or notification hardware, this solution costs nothing, takes under a minute to set up, and works through the auditory channel — which means your eyes stay free.

---

## Design Notes

### Two Sounds, Two States

The plugin uses two distinct audio cues to communicate two different states:

- **Glass** (a clean, high-pitched chime) — plays when Claude finishes a task. It signals completion: calm, clear, no urgency. You can wrap up what you're doing before returning.

- **Ping** (a short, sharper tone) — plays when Claude needs your authorization to proceed. It signals a pause in execution: something is waiting on you specifically. This is the one to respond to promptly.

### Volume: Louder Than Your System Setting

The alerts play at **3× your current system volume**, not at the system level.

This is deliberate. In office environments, most people keep their computer volume low — quiet enough not to disturb colleagues, quiet enough that a standard notification sound would go unnoticed with headphones off or music on. A notification that doesn't actually get your attention defeats the purpose.

By amplifying independently of the system slider, the alerts stay audible across typical working conditions without requiring you to change your normal volume settings.

Each sound is also accompanied by a standard **system notification banner**, so if you're in a quiet environment and miss the audio, you can catch it in your Notification Center as well.

---

## Installation

1. Double-click `notify-on-stop.skill` to install it in Claude Code.
2. Claude will detect your OS and write the appropriate hooks into `~/.claude/settings.json` automatically.
3. **Fully quit and relaunch Claude Code.** Hooks are loaded at startup — if Claude Code was already running when the hooks were written, it won't pick them up until you restart. This applies to all platforms.

**macOS only:** After installation, go to **System Settings → Notifications → Claude** (or your terminal app) and make sure **Sounds** is enabled. The audio will still play regardless, but this ensures the banner notification also makes a sound of its own.

**Supported platforms:** macOS, Linux, Windows.

---

## Uninstalling

There are two layers to uninstall, in order of importance:

**1. Remove the notification hooks (stops all alerts)**

This is the part that actually makes noise. Ask Claude directly: *"Remove the notify-on-stop hooks from my settings"* — it will open `~/.claude/settings.json` and delete the `Stop` and `Notification` hook entries for you.

Alternatively, open `~/.claude/settings.json` in any text editor and manually delete the `Stop` and `Notification` blocks inside `"hooks"`. If those are the only hooks you have, you can remove the entire `"hooks"` key.

**2. Uninstall the skill itself (optional)**

The skill file is just a set of instructions — it does nothing on its own unless the hooks are active. If you'd like to remove it anyway, run `/skills` inside Claude Code and uninstall *notify-on-stop* from there.


---

---

# notify-on-stop

**为 Claude Code 添加任务完成提醒：桌面通知 + 音效**

---

## 为什么需要它：注意力也是稀缺资源

用 Claude Code 或其他 AI Agent 跑任务时，有一个典型的困境：你不知道任务什么时候跑完。于是你开始每隔几分钟切回终端窗口看一眼，确认还在跑，然后再切回去继续自己的事。

这个代价不小。如果把人脑也视为一个 Agent，每一次不必要的上下文切换都在消耗工作记忆和认知带宽。那一眼"随便看看"并不是免费的——它打断了心流，让你无法真正进入专注状态，日积月累会形成真实的疲劳。

有了声音提醒，等待时间可以用两种更好的方式度过：

- **全身心投入另一件事。** 开启通知之后，你可以把注意力完整地交给另一项任务——写作、阅读、开会——不需要留一部分 context 去监视 Agent。任务结束或需要授权的那一刻，你会立刻收到提示。

- **真正休息一下。** 闭上眼睛，冥想，让大脑恢复。这件事在"一边刷手机一边时不时瞄一眼运行窗口"的状态下几乎无法实现——那种状态反而更累。声音提醒让你可以真正离开屏幕，把"监视"的任务交给耳朵，认知 context 得以真正清空复位

相比红绿灯等外部硬件设备，这套方案零成本、一分钟内完成部署，并且通过听觉通道传递信息，为视觉系统减负。

---

## 设计说明

### 两种音效，两种状态

插件使用两个不同的音效，对应两种不同的状态：

- **Glass**（清脆的高频短音）——Claude 完成任务时播放。信号含义：已结束，不紧急，你可以把手头的事做完再回来看。

- **Ping**（短促、略尖锐的提示音）——Claude 等待你授权时播放。信号含义：执行暂停，需要你操作。这个声音响了，最好尽快回来。

### 音量：比系统设置更响

提示音的播放音量是**系统音量的 3 倍**，而不是跟着系统走。

这也是有意为之。办公场合里，大多数人的电脑音量调得很低——低到不打扰同事，低到摘下耳机时系统通知音几乎听不见。如果提示音根本没被注意到，整个方案就失去了意义。

独立放大音量，可以让提示音在典型的办公环境里保持清晰可闻，同时不影响你平时的音量习惯。

每次提示音响起的同时，也会弹出一条**系统通知横幅**。如果你处于安静环境、没听见声音，也可以在通知中心里补看。

---

## 安装方法

1. 双击 `notify-on-stop.skill`，安装到 Claude Code。
2. Claude 会自动检测你的操作系统，并将对应的 hook 写入 `~/.claude/settings.json`。
3. **完全退出并重新启动 Claude Code。** Hooks 在启动时加载——如果写入配置时 Claude Code 已在运行，必须重启才能生效。所有平台均适用。

**macOS 用户注意：** 安装完成后，前往**系统设置 → 通知 → Claude**（或运行 Claude Code 的终端 App），确认**声音**开关已打开。这一步不影响 `afplay` 的音效播放，但能保证通知横幅本身也有提示音。

**支持平台：** macOS、Linux、Windows。

---

## 卸载方法

卸载分两层，按重要性排序：

**1. 移除通知 hooks（关掉所有提示音和通知）**

这是真正"发出声音"的部分。直接告诉 Claude：*"帮我移除 notify-on-stop 的 hooks"*——它会打开 `~/.claude/settings.json`，自动删除其中的 `Stop` 和 `Notification` hook 条目。

**2. 卸载 skill 本身（可选）**

Skill 文件只是一段指令，没有激活 hooks 的情况下它不会主动做任何事。如果你也想彻底清掉，在 Claude Code 里运行 `/skills`，找到 *notify-on-stop* 卸载即可。
