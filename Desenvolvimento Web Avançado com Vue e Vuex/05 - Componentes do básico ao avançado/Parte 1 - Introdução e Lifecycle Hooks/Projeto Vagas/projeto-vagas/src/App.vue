<!-- @format -->

<template>
  <div>
    <h1>Componente App</h1>
    <button @click="desmontarComponente()">
      Desmontar o componente Conteudo
    </button>
    <Topo />
    <Conteudo v-if="visibilidade" />
  </div>
</template>

<script>
import Conteudo from "./components/layouts/Conteudo.vue";
import Topo from "./components/layouts/Topo.vue";

export default {
  name: "App",
  data: () => ({
    visibilidade: true,
  }),
  components: {
    Conteudo,
    Topo,
  },
  methods: {
    desmontarComponente() {
      this.visibilidade = false;
    },
  },
};
</script>

<style scoped></style>
