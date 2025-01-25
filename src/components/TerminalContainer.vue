<script setup lang="ts">
  import { ref, onMounted } from 'vue';
  import { Terminal } from '@xterm/xterm';
  import { FitAddon } from '@xterm/addon-fit';
  import '@xterm/xterm/css/xterm.css';

  const terminal = ref<Terminal | null>(null);
  const terminalContainer = ref<HTMLElement | null>(null);

  const initializeTerminal = () => {
    terminal.value = new Terminal({
      cursorBlink: true,
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
