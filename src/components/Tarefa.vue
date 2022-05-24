<template>
  <box-padrao>
    <div class="columns">
      <div class="column is-7">
        {{ tarefa.descricao || "Descrição não definida" }}
      </div>
      <div class="column">
        <cronometro-timer :tempoEmSegundos="tarefa.duracaoEmSegundos" />
      </div>
    </div>
  </box-padrao>
</template>

<script lang="ts">
import ITarefa from "@/interfaces/ITarefa";
import { defineComponent, PropType } from "vue";
import CronometroTimer from "./Cronometro.vue";
import BoxPadrao from "./BoxPadrao.vue";

export default defineComponent({
  name: "TarefaDescricao",
  components: {
    CronometroTimer,
    BoxPadrao,
  },
  props: {
    tarefa: {
      type: Object as PropType<ITarefa>,
      required: true,
    },
  },
});
</script>
