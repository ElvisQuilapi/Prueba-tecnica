<template>
  <div class="busqueda">
    <input type="text" placeholder="Búsqueda" v-model="elementoBusqueda" />
  </div>
</template>

<script>
export default {
  name: "busqueda-heroes",
  data() {
    return {
      elementoBusqueda: "",
    };
  },
  watch: {
    elementoBusqueda(v) {
      this.$emit("input", v);
    },
  },
};
</script>
<style lang="scss" scoped>
.busqueda {
  width: 100%;
  display: block;
  input[type=text] {
    width: calc(100% - 15px);
    height: 34px;
    padding: 0 5px;
    outline: none;
    border-color: solid 1px #f6f6f6;
  }
}
</style>