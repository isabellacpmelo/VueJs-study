<!-- @format -->

<template>
  <slot name="titulo" :dadosTitulo="{ titulo: 'Titulo Lista', nroVagas: 15 }">
    <p>Titulo da lista de vagas</p>
  </slot>
  <slot :vagas="vagas">
    <div v-for="(vaga, index) in vagas" :key="index" class="row mt-5">
      <div class="col">
        <Vaga v-bind="vaga" />
      </div>
    </div>
  </slot>
  <slot
    name="rodape"
    :dadosTitulo="{
      titulo: 'Rodapé Lista',
      paginacao: { nroPaginas: 10, paginaAtual: 5 },
    }">
    <p>O rodape da lista de vagas</p>
  </slot>
</template>

<script>
import Vaga from "@/components/comuns/Vaga.vue";

export default {
  name: "ListaVagas",
  components: {
    Vaga,
  },
  data: () => ({
    vagas: [],
  }),
  // Se não existisse o keep alive, seria mounted()
  activated() {
    this.vagas = JSON.parse(localStorage.getItem("vagas"));
  },
  mounted() {
    this.emitter.on("filtrarVagas", (vaga) => {
      const vagas = JSON.parse(localStorage.getItem("vagas"));

      //true ou false: O método filter cria um novo array com todos os elementos que passaram no teste implementado na função.
      this.vagas = vagas.filter((reg) =>
        reg.titulo.toLowerCase().includes(vaga.titulo.toLowerCase())
      );
    });
  },
};
</script>
