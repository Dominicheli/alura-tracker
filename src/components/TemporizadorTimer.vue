<template>
  <div class="is-flex is-align-items-center is-justify-content-space-between">
    <cronometro-timer :tempoEmSegundos="tempoEmSegundos" />
    <Button
      @clicado="iniciar"
      icone="fas fa-play"
      texto="play"
      :desabilitado="cronometroRodando"
      >play</Button
    >
    <Button
      @clicado="finalizar"
      icone="fas fa-stop"
      texto="stop"
      :desabilitado="!cronometroRodando"
      >stop</Button
    >
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import CronometroTimer from "./Cronometro.vue";
import BotaoAcao from "./BotaoAcao.vue";

export default defineComponent({
  name: "TemporizadorTimer",
  emits: ["aoTemporizadorFinalizado"],
  components: {
    CronometroTimer,
    Button: BotaoAcao,
  },
  data() {
    return {
      tempoEmSegundos: 0,
      cronometro: 0,
      cronometroRodando: false,
    };
  },

  methods: {
    iniciar() {
      // começar a contagem
      // 1 seg = 1000 ms
      this.cronometroRodando = true;
      this.cronometro = setInterval(() => {
        this.tempoEmSegundos += 1;
      }, 1000);
    },
    finalizar() {
      this.cronometroRodando = false;
      clearInterval(this.cronometro);
      this.$emit("aoTemporizadorFinalizado", this.tempoEmSegundos);
      this.tempoEmSegundos = 0;
    },
  },
});
</script>
