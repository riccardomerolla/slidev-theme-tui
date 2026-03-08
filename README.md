# slidev-theme-tui

> Terminal User Interface theme for [Slidev](https://sli.dev) - Inspired by **vi**, **nano**, **emacs**, **htop**, and **Gemini CLI**

![Version](https://img.shields.io/npm/v/slidev-theme-tui)
![License](https://img.shields.io/npm/l/slidev-theme-tui)

## Features

- Phosphor green CRT terminal aesthetic with scanline effects
- 5 unique layouts: `default`, `cover`, `terminal`, `vim`, `htop`, `gemini`
- Gemini CLI inspired layout with purple/blue AI aesthetic
- Reusable Vue components: `StatusBar`, `TerminalWindow`, `GeminiPrompt`
- Animated CRT scanlines, phosphor glow, and matrix background effects
- Multiple color schemes: green phosphor, amber, blue terminal
- JetBrains Mono / Fira Code monospace fonts
- Box-drawing characters for authentic TUI borders
- Cursor blink animations and typewriter effects

## Install

```bash
npm install slidev-theme-tui
```

## Usage

Add `theme: tui` to your slides frontmatter:

```yaml
---
theme: tui
title: My TUI Presentation
---
```

## Layouts

### `default`
Standard layout with phosphor green status bar, top bar, and CRT scanlines.

### `cover`
Full-screen cover with ASCII art box, matrix background, and blinking cursor.

### `terminal`
MacOS-style terminal window with colored dots, bash prompt, and scrollable content.

### `vim`
Authentic vim editor with line numbers gutter, tab bar, status line, and command line.

### `htop`
Process monitor-style layout with CPU/memory bars, process table, and F-key footer.

### `gemini`
Gemini CLI inspired layout with gradient header, purple/teal AI aesthetic.

## Components

### `<TerminalWindow>`

```vue
<TerminalWindow
  title="my-app -- bash"
  user="riccardo"
  host="devbox"
  path="~/projects"
  command="npm run dev"
>
  Your content here
</TerminalWindow>
```

### `<GeminiPrompt>`

```vue
<GeminiPrompt prompt="Explain microservices">
  Microservices are an architectural style...
</GeminiPrompt>
```

### `<StatusBar>`

```vue
<StatusBar mode="NORMAL" file="slides.md" :show-page="true" :page="1" />
```

## Color Schemes

Apply via CSS class on any element or layout:

| Class | Scheme |
|---|---|
| (default) | Phosphor Green `#33ff66` |
| `bg-amber` | Amber Phosphor `#ffb700` |
| `bg-blue-terminal` | Blue Terminal `#66ccff` |
| `layout-gemini` | Gemini AI `#818cf8` |

## Background Effects

| Class | Effect |
|---|---|
| `bg-matrix` | Scrolling binary/ASCII matrix |
| `bg-scanlines` | CRT horizontal scanlines |
| `bg-vignette` | CRT edge darkening |
| `bg-ascii` | Monospace grid pattern |
| `bg-noise` | CRT noise animation |
| `bg-gemini` | Gemini gradient radials |

## Project Structure

```
slidev-theme-tui/
├── layouts/
│   ├── default.vue
│   ├── cover.vue
│   ├── terminal.vue
│   ├── vim.vue
│   ├── htop.vue
│   └── gemini.vue
├── components/
│   ├── StatusBar.vue
│   ├── TerminalWindow.vue
│   └── GeminiPrompt.vue
├── styles/
│   ├── base.css
│   ├── gemini.css
│   └── backgrounds.css
├── example.md
└── package.json
```

## License

MIT License - [Riccardo Merolla](https://github.com/riccardomerolla)
