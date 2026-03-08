---
theme: ./
title: slidev-theme-tui Demo
info: Terminal User Interface theme for Slidev
highlighter: shiki
colorSchema: dark
---

# slidev-theme-tui

Terminal UI theme inspired by **vi**, **nano**, **htop**, and **Gemini CLI**

<div class="tui-animate-in" style="margin-top: 1rem;">

```bash
$ npm install slidev-theme-tui
$ slidev --theme tui presentation.md
```

</div>

---
layout: terminal
---

## Terminal Layout

Authentic terminal window with macOS-style dots

```bash
$ ls -la
total 48
drwxr-xr-x  8 user staff  256 Mar  8 14:00 .
drwxr-xr-x 12 user staff  384 Mar  8 13:55 ..
-rw-r--r--  1 user staff 1234 Mar  8 14:00 package.json
drwxr-xr-x  6 user staff  192 Mar  8 14:00 layouts/
drwxr-xr-x  3 user staff   96 Mar  8 14:00 components/
drwxr-xr-x  3 user staff   96 Mar  8 14:00 styles/
```

---
layout: vim
---

## Vim Layout

- Line numbers in the gutter
- Tab bar at the top
- Authentic vim status line at the bottom
- Command line area

> Press `:wq` to save and quit your presentation

---
layout: nano
---

## GNU Nano Layout

A lightweight text editor inspired theme:

- Traditional nano top bar with file information
- Clean content editing area
- Help footer with keyboard shortcuts

> Press `^X` to exit your presentation

---
layout: htop
htopTitle: Your custom htop title here
---

Your custom htop content here **Agent AI**

---
layout: gemini
---

<GeminiPrompt prompt="Explain the TUI theme architecture for Slidev">

The `slidev-theme-tui` is built with **three layers**:

1. **CSS custom properties** — phosphor green color system with CRT effects
2. **Layout components** — vim, htop, terminal, gemini-inspired frames
3. **Vue components** — reusable StatusBar, TerminalWindow, GeminiPrompt

</GeminiPrompt>

---
layout: default
---

## Components

Use components anywhere in your slides:

```vue
<!-- Reusable terminal window -->
<TerminalWindow title="bash" user="riccardo" host="devbox" path="~/projects">
  npm install slidev-theme-tui
</TerminalWindow>

<!-- AI conversation block -->
<GeminiPrompt prompt="Write a Scala ZIO service">
  Here is a ZIO service example...
</GeminiPrompt>

<!-- Status bar -->
<StatusBar mode="NORMAL" file="slides.md" :show-page="true" :page="1" />
```

---
layout: cover
---

# Thank You

<template #info>

Made with `slidev-theme-tui` &bull; MIT License

[github.com/riccardomerolla/slidev-theme-tui](https://github.com/riccardomerolla/slidev-theme-tui)

</template>
