<template>
  <div class="lista-heroes">
    <lista-heroes :elementos="heroes" @visualizarHero="verDetalle($event)"/>
    <detalle-hero :elemento="itemHero" :loading="cargaHero"/>
  </div>
</template>

<script>
import listaHeroes from "./components/lista-heroes";
import detalleHero from "./components/detalle-hero";
import axios from "axios";
export default {
  name: "Home",
  data() {
    return {
      vistaHero: false,
      cargaHero: false,
      heroes: [],
      itemHero: [],
      url: "http://157.245.138.232:9091/api/v1/test/",
    };
  },
  created() {
    this.buscarDatos();
  },
  methods: {
    buscarDatos() {
      axios
        .get(this.url + `superheroes`)
        .then((response) => {
          const { data } = response.data;
          this.heroes = data;
        })
        .catch((error) => {
          console.log(error);
        });
    },
    verDetalle(id) {
      this.vistaHero = true
      this.itemHero = []
      this.cargaHero = true;
      axios.get(this.url + `superheroes/${id}`).then((response) => {
        this.cargaHero = false;
        const { data } = response.data;
        this.itemHero = data;
      });
    },
  },
  components: {
    listaHeroes,
    detalleHero
  },
};
</script>

<style lang="scss" scoped>
.lista-heroes {
  width: 480px;
  margin: 4em auto;
}
</style>