<h1 align="center">notify-on-stop</h1>

<p align="center">
  <strong>Desktop notifications + sound alerts for AI agents</strong><br>
  <sub>Claude Code · OpenAI Codex CLI · Tencent WorkBuddy</sub>
</p>

<p align="center">
  <strong>English</strong> · <a href="../README.md">中文</a>
</p>

---

## The Problem: Your Attention Is a Finite Resource

When you kick off a long task in Claude Code or any AI agent, you face a familiar dilemma: you don't know when it'll finish. So you end up context-switching every few minutes — alt-tabbing back to the terminal, glancing at the screen, then returning to whatever you were doing. Rinse and repeat.

This is costly. If you treat the human brain as an agent of its own, every unnecessary context switch consumes working memory and drains cognitive bandwidth. That idle glance isn't free — it interrupts your flow, breaks your concentration, and accumulates into real fatigue over the course of a day.

There are two better ways to spend that waiting time:

- **Go deep on something else.** With notifications enabled, you can fully commit to another task — writing, reading, a conversation — without reserving any mental capacity to monitor the agent. You get notified the moment it's done or needs your input.

- **Actually rest.** Close your eyes. Meditate. Let your mind recover. This is almost impossible to do when you're half-watching a terminal window and half-scrolling through your phone "just in case." With audio alerts, you can genuinely step away from screens and let your auditory system take the watch — freeing up your cognitive context to actually reset, not just idle.

Compared to purpose-built attention devices like traffic lights or notification hardware, this solution costs nothing, takes under a minute to set up, and works through the auditory channel — which means your eyes stay free.

---

## Design Notes

### Two Sounds, Two States

The plugin uses two distinct audio cues to communicate two different states:

- **Glass** (a clean, high-pitched chime) — plays when Claude finishes a task. It signals completion: calm, clear, no urgency. You can wrap up what you're doing before returning.

- **Ping** (a short, sharper tone) — plays when Claude needs your authorization to proceed. It signals a pause in execution: something is waiting on you specifically. This is the one to respond to promptly.

The difference in timbre is intentional. Over time, you'll recognize them without thinking — the same way you can tell a doorbell from a smoke alarm without looking.

### Volume: Louder Than Your System Setting

The alerts play at **3× your current system volume**, not at the system level.

This is deliberate. In office environments, most people keep their computer volume low — quiet enough not to disturb colleagues, quiet enough that a standard notification sound would go unnoticed with headphones off or music on. A notification that doesn't actually get your attention defeats the purpose.

By amplifying independently of the system slider, the alerts stay audible across typical working conditions without requiring you to change your normal volume settings.

Each sound is also accompanied by a standard **system notification banner**, so if you're in a quiet environment and miss the audio, you can catch it in your Notification Center as well.

---

## Installation

1. Download [`notify-on-stop.skill`](../notify-on-stop.skill) and double-click to install it in Claude Code.
2. In a Claude Code session, say: *"Set up completion notifications"* — or just run `/notify-on-stop`.
3. Claude will detect which tools you have installed and write hooks into each one's config file:

| Tool | Config file |
|------|-------------|
| Claude Code | `~/.claude/settings.json` |
| OpenAI Codex CLI | `~/.codex/hooks.json` |
| Tencent WorkBuddy | `~/.codebuddy/settings.json` |

4. **Fully quit and relaunch each tool.** Hooks are loaded at startup — a restart is required for changes to take effect.

**macOS only:** After installation, go to **System Settings → Notifications** and make sure **Sounds** is enabled for each app. The audio plays regardless, but this ensures the banner also chimes.

**Supported platforms:** macOS, Linux, Windows.

---

## Uninstalling

There are two layers to uninstall, in order of importance:

**1. Remove the notification hooks (stops all alerts)**

This is the part that actually makes noise. Ask Claude directly: *"Remove the notify-on-stop hooks from my settings"* — it will open `~/.claude/settings.json` and delete the `Stop` and `Notification` hook entries for you.

Alternatively, open `~/.claude/settings.json` in any text editor and manually delete the `Stop` and `Notification` blocks inside `"hooks"`. If those are the only hooks you have, you can remove the entire `"hooks"` key.

**2. Uninstall the skill itself (optional)**

The skill file is just a set of instructions — it does nothing on its own unless the hooks are active. If you'd like to remove it anyway, run `/skills` inside Claude Code and uninstall *notify-on-stop* from there.
