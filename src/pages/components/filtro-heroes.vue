<template>
  <div class="opciones-filtro">
    <h4>Filtrar</h4>
    <div class="radio-grupo">
      <label for="vuelan">
        <input type="radio" :value="true" v-model="tipoHero" id="vuelan" />
        Si vuelan
      </label>
      <label for="no-vuelan">
        <input type="radio" :value="false" v-model="tipoHero" id="no-vuelan" />
        No vuelan
      </label>
      <button @click="tipoHero = null" :disabled="!isDisabled">Limpiar</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "filtro-heroes",
  data() {
    return {
      tipoHero: null,
    };
  },
  watch: {
    tipoHero() {
      this.$emit("input", this.tipoHero);
    },
  },
  computed: {
    isDisabled() {
      if (this.tipoHero != null) {
        return true;
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.opciones-filtro {
  display: flex;
  align-items: center;
  justify-content: flex-start;
  flex-direction: row;

  h4 {
    font-size: 12px;
  }

  .radio-grupo {
    margin-left: 15px;

    label {
      font-size: 12px;
    }
  }

  button {
    border: solid 1px #333;
    margin-left: 10px;
    font-size: 12px;
    padding: 2px 5px;
    border-radius: 3px;
    color: #333;
    outline: none;
    &:hover {
      cursor: pointer;
      background-color:  #f0f0f0;
      border: solid 1px #9b9b9b;
    }

    &:disabled {
      cursor: not-allowed;
      background-color:  #f0f0f07b;
      border: solid 1px #cbcbcb;
    }
  }

}
</style>