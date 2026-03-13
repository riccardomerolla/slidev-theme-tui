<template>
  <div class="slidev-layout borland">
    <!-- Top Menu Bar -->
    <div class="tui-topbar">
      <span class="menu-item"><span>F</span>ile</span>
      <span class="menu-item active"><span>E</span>dit</span>
      <span class="menu-item"><span>S</span>earch</span>
      <span class="menu-item"><span>R</span>un</span>
      <span class="menu-item"><span>C</span>ompile</span>
      <span class="menu-item"><span>D</span>ebug</span>
      <span class="menu-item"><span>P</span>roject</span>
      <span class="menu-item"><span>O</span>ptions</span>
      <span class="menu-item"><span>W</span>indow</span>
      <span class="menu-item"><span>H</span>elp</span>
    </div>

    <!-- Main Window Area -->
    <div class="tui-content-wrapper">
      <div class="tui-window">
        <div class="tui-window-header">
          <span class="close-btn">[■]</span>
          <span class="title"> {{ windowTitle || 'NONAME00.CPP' }} </span>
          <span class="zoom-btn">[↕]</span>
        </div>
        <div class="tui-window-content">
          <slot />
        </div>
      </div>
    </div>

    <!-- Status Bar -->
    <div class="tui-statusbar">
      <span class="shortcut"><span class="key">F1</span><span class="label">Help</span></span>
      <span class="shortcut"><span class="key">F2</span><span class="label">Save</span></span>
      <span class="shortcut"><span class="key">F3</span><span class="label">Open</span></span>
      <span class="shortcut"><span class="key">Alt-F9</span><span class="label">Compile</span></span>
      <span class="shortcut"><span class="key">F9</span><span class="label">Make</span></span>
      <span class="shortcut"><span class="key">F10</span><span class="label">Menu</span></span>
    </div>
  </div>
</template>

<script setup>
defineProps({
  windowTitle: {
    type: String,
    default: 'NONAME00.CPP'
  }
})
</script>
