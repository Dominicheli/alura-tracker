<template>
  <main
    class="columns is-gapless is-multiline"
    :class="{ 'modo-escuro': modoEscuroAtivo }"
  >
    <div class="column is-one-quarter">
      <barra-lateral @aoTemaAlterado="trocarTema" />
    </div>
    <div class="column is-three-quarter conteudo">
      <barra-formulario @aoSalvarTarefa="salvarTarefa" />
      <div class="lista">
        <tarefa-descricao
          v-for="(tarefa, index) in tarefas"
          :key="index"
          :tarefa="tarefa"
        />
        <box-padrao v-if="listaEstaVazia">
          Nenhuma tarefa feita ainda! :(
        </box-padrao>
      </div>
    </div>
  </main>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import BarraLateral from "./components/BarraLateral.vue";
import BarraFormulario from "./components/BarraFormulario.vue";
import TarefaDescricao from "./components/Tarefa.vue";
import ITarefa from "./interfaces/ITarefa";
import BoxPadrao from "./components/BoxPadrao.vue";
export default defineComponent({
  name: "App",
  components: {
    BarraLateral,
    BarraFormulario,
    TarefaDescricao,
    BoxPadrao,
  },
  data() {
    return {
      tarefas: [] as ITarefa[],
      modoEscuroAtivo: false,
    };
  },
  computed: {
    listaEstaVazia(): boolean {
      return this.tarefas.length === 0;
    },
  },
  methods: {
    salvarTarefa(tarefa: ITarefa) {
      this.tarefas.push(tarefa);
    },
    trocarTema(modoEscuroAtivo: boolean) {
      this.modoEscuroAtivo = modoEscuroAtivo;
    },
  },
});
</script>

<style>
.lista {
  padding: 1.25rem;
}
main {
  --bg-primario: #fff;
  --texto-primario: #000;
}
main.modo-escuro {
  --bg-primario: #2b2d42;
  --texto-primario: rgb(116, 116, 116);
}
.conteudo {
  background-color: var(--bg-primario);
}
</style>
