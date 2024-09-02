<script lang="ts">
import { obterReceitas } from "@/http";
import type IReceita from "@/interface/IReceita";
import BotaoPrincipal from "@/components/BotaoPrincipal.vue";
import CardReceita from "@/components/CardReceita.vue";

export default {
  data(){
    return{
      receitasEncontradas: [] as IReceita[]
    }
  },
  async created(){
    const receitas = await obterReceitas();
    this.receitasEncontradas = receitas.slice(0, 8);
  },
  components: {BotaoPrincipal, CardReceita},
  emits: ['editarReceitas']
}

</script>

<template>
  <section class="mostrar-receitas">
    <h1 class="cabecalho titulo-receitas">Receitas</h1>

    <p class="paragrafo-lg resultados-encontrados">
      Resultados encontrados: {{receitasEncontradas.length}}
    </p>

    <div v-if="receitasEncontradas.length" class="receitas-wrapper">
      <p class="paragrafo-lg informacoes">
        Veja as opções de receitas que encontramos para você, com os ingredientes que tem por ai!
      </p>

      <ul class="receitas">
      <li v-for="receita of receitasEncontradas" :key="receita.nome">
        <CardReceita :receita="receita" />
      </li>

      </ul>

    </div>

  </section>
</template>

<style scoped>
.mostrar-receitas {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
}

.titulo-receitas {
  color: var(--verde-medio, #3D6D4A);
  margin-bottom: 1.5rem;
}

.resultados-encontrados {
  color: var(--verde-medio, #3D6D4A);
  margin-bottom: 0.5rem;
}

.receitas-wrapper {
  margin-bottom: 3.5rem;
}

.informacoes {
  margin-bottom: 2rem;
}

.receitas {
  display: flex;
  justify-content: center;
  gap: 1.5rem;
  flex-wrap: wrap;
}

.receitas-nao-encontradas {
  margin-bottom: 2rem;
}

.receitas-nao-encontradas__info {
  margin-bottom: 0.5rem;
}

@media only screen and (max-width: 767px) {
  .receitas-wrapper {
    margin-bottom: 2rem;
  }
}
</style>