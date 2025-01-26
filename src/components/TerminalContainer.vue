<script setup lang="ts">
  import { ref, onMounted, watch } from 'vue';
  import { useCssVar, useMediaQuery } from '@vueuse/core';
  import { Terminal } from '@xterm/xterm';
  import { FitAddon } from '@xterm/addon-fit';
  import '@xterm/xterm/css/xterm.css';

  const terminalTheme = ref({
    selection: '#97979b33',
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
  });

  const prefersColorScheme = useMediaQuery('(prefers-color-scheme: light)');

  watch(
    prefersColorScheme,
    () => {
      const dynamicTheme = {
        foreground: useCssVar('--color-text').value,
        background: useCssVar('--color-background-soft').value,
        black: useCssVar('--vt-c-black').value,
        brightBlack: useCssVar('--vt-c-black-mute').value,
        white: useCssVar('--vt-c-white-mute').value,
        brightWhite: useCssVar('--vt-c-white').value,
      };
      terminalTheme.value = {
        ...terminalTheme.value,
        ...dynamicTheme,
      };
    },
    { immediate: true },
  );

  watch(terminalTheme, (newTheme) => {
    if (terminal.value) {
      terminal.value.options.theme = newTheme;
    }
  });

  const terminal = ref<Terminal | null>(null);
  const terminalContainer = ref<HTMLElement | null>(null);

  const initializeTerminal = () => {
    terminal.value = new Terminal({
      cursorBlink: true,
      theme: terminalTheme.value,
      fontFamily: 'CaskaydiaCove',
      fontWeight: 300,
      fontWeightBold: 700,
      fontSize: 16,
    });
    const fitAddon = new FitAddon();
    terminal.value.loadAddon(fitAddon);
    terminal.value.open(terminalContainer.value!);
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
  <div id="terminal-border">
    <div ref="terminalContainer" id="terminal-container"></div>
  </div>
</template>

<style>
  .xterm-viewport::-webkit-scrollbar {
    width: 8px;
  }

  .xterm-viewport::-webkit-scrollbar-track {
    background: var(--color-border);
  }

  .xterm-viewport::-webkit-scrollbar-thumb {
    background: var(--color-border-hover);
    border-radius: 4px;
  }

  #terminal-border {
    width: 50vw;
    height: 50vh;
    padding: 2px;
    border-radius: 1rem;
    overflow: hidden;
    position: relative;
  }

  #terminal-container {
    width: 100%;
    height: 100%;
    background-color: var(--color-background-soft);
    border-radius: 1rem;
    overflow: hidden;
  }

  #terminal-container > .xterm {
    height: 100%;
    padding: 8px;
  }

  #terminal-border::after {
    content: '';
    position: absolute;
    width: 75vmax;
    height: 75vmax;
    left: 50%;
    top: 50%;
    background: conic-gradient(#3a4ed5, var(--color-raspberry), #3a4ed5);
    z-index: -1;
    animation: rotate 10s linear infinite;
  }

  @keyframes rotate {
    from {
      transform: translate(-50%, -50%) rotate(0deg);
    }
    to {
      transform: translate(-50%, -50%) rotate(360deg);
    }
  }
</style>
