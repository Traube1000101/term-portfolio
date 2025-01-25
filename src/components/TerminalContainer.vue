<script lang="ts">
  import { Terminal } from '@xterm/xterm';
  import { FitAddon } from '@xterm/addon-fit';
  import '@xterm/xterm/css/xterm.css';

  export default {
    name: 'XtermTerminal',
    data() {
      return {
        terminal: null,
      };
    },
    mounted() {
      this.initializeTerminal();
    },
    methods: {
      initializeTerminal() {
        this.terminal = new Terminal({
          cursorBlink: true,
        });
        const fitAddon = new FitAddon();
        this.terminal.loadAddon(fitAddon);
        this.terminal.open(this.$refs.terminalContainer);
        fitAddon.fit();

        this.terminal.writeln('This is a Terminal :3');
      },
    },
  };
</script>

<template>
  <div ref="terminalContainer"></div>
</template>
