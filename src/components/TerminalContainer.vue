<script setup lang="ts">
  import { ref, onMounted } from 'vue';
  import { useCssVar } from '@vueuse/core';
  import { Terminal } from '@xterm/xterm';
  import { FitAddon } from '@xterm/addon-fit';
  import '@xterm/xterm/css/xterm.css';

  const terminalTheme = {
    foreground: useCssVar('--color-text').value,
    background: useCssVar('--color-background-soft').value,
    selection: '#97979b33',
    black: useCssVar('--vt-c-black').value,
    brightBlack: useCssVar('--vt-c-black-mute').value,
    red: '#ff5c57',
    brightRed: '#ff5c57',
    green: '#5af78e',
    brightGreen: '#5af78e',
    yellow: '#f3f99d',
    brightYellow: '#f3f99d',
    blue: '#57c7ff',
    brightBlue: '#57c7ff',
    magenta: '#ff6ac1',
    brightMagenta: '#ff6ac1',
    cyan: '#9aedfe',
    brightCyan: '#9aedfe',
    white: useCssVar('--vt-c-white-mute').value,
    brightWhite: useCssVar('--vt-c-white').value,
  };

  const terminal = ref<Terminal | null>(null);
  const terminalContainer = ref<HTMLElement | null>(null);

  const initializeTerminal = () => {
    terminal.value = new Terminal({
      cursorBlink: true,
      theme: terminalTheme,
    });
    const fitAddon = new FitAddon();
    terminal.value.loadAddon(fitAddon);
    terminal.value.open(terminalContainer.value);
    fitAddon.fit();

    terminal.value.writeln('This is a Terminal :3');
  };

  onMounted(() => {
    if (terminalContainer.value) {
      initializeTerminal();
    }
  });
</script>

<template>
  <div ref="terminalContainer"></div>
</template>
