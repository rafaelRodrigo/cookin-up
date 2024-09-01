<script lang="ts">
import Tag from "./Tag.vue";
export default {
  components: { Tag },
  props:{
    ingrediente: {type: String, required: true}
  },
  data(){
    return{
      selecionado: false
    }
  },
  methods:{
    aoClicar(){
      this.selecionado = !this.selecionado
      if (this.selecionado){
        this.$emit('adicionarIngrediente',this.ingrediente);
      }else{
        this.$emit('removeIngrediente',this.ingrediente);
      }
    }
  },
  emits:['adicionarIngrediente','removeIngrediente']
}
</script>

<template>
  <!--v-on:click="selecionado = !selecionado"-->
  <!-- @:click="selecionado = !selecionado" -->
  <button
    class="ingrediente"
    @:click="aoClicar"
    :aria-pressed="selecionado"
  >
    <Tag :texto="ingrediente" :ativa="selecionado"/>
  </button>
</template>

<style scoped>
.ingrediente{
  cursor: pointer;
}

</style>