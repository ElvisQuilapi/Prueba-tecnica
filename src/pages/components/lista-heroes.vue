<template>
  <div>
    <!-- Búsqueda -->
    <busqueda-heroes v-model="elementoBusqueda"/>
    <!-- Filtrar heroes -->
    <filtro-heroes v-model="tipoHero" />

    <!-- Lista de heroes -->
    <div class="panel-heroes">
      <div class="encanbezado">
        <h3>Superhéroes</h3>
      </div>
      <ul>
        <li v-if="!filterHeroes.length" class="sin-elementos">Upa! No se encontraron los elementos.</li>
        <li v-for="(elemento, idx) in filterHeroes" :key="idx" @click="detalleHero(elemento.id, idx)" :class=" {claseHero : idx == activeHero} ">
          <div class="avatar">
            <img :src="elemento.avatarURL" :alt="elemento.nombre" />
          </div>
          <div class="descripcion">
            <h3>{{ elemento.nombre }}</h3>
            <small>{{ elemento.nombreReal }}</small>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import filtroHeroes from "./filtro-heroes";
import busquedaHeroes from "./busqueda-heroes";

export default {
  name: "Lista-heroes",
  props: {
    elementos: {
      type: [Array, Object]
    },
  },
  data() {
    return {
      tipoHero: null,
      elementoBusqueda: "",
      activeHero: null
    };
  },
  methods: {
    detalleHero(id, indice) {
      this.activeHero = indice
      this.$emit('visualizarHero', id)
    }
  },
  computed: {
    filterHeroes() {
      if (this.elementoBusqueda) {
        return this.elementos.filter((elm) => {
          console.log(elm)
          return this.elementoBusqueda
            .toLowerCase()
            .split(" ")
            .every((v) => elm.nombre.toLowerCase().includes(v));
        });
      }

      if (this.tipoHero != null) {
        return this.elementos.filter(
          (h) => h.puedeVolar === Boolean(this.tipoHero)
        );
      }
    
      else {
        return this.elementos;
      }
    },
  },
  components: {
    filtroHeroes,
    busquedaHeroes
  },
};
</script>

<style lang="scss" scoped>
.claseHero {
  background-color: #efefef;
}
.panel-heroes {
  background-color: #fff;
  border: solid 1px #ddd;
  border-radius: 3px;

  .sin-elementos {
    font-size: 12px;
  }

  .encanbezado {
    background-color: #f0f0f0;
    padding: 10px;
    h3 {
      margin: 0;
    }
  }

  ul {
    list-style: none;
    margin: 0;
    padding: 0;
    border-radius: 3px;
    li {
      display: flex;
      align-items: center;
      flex-direction: row;
      justify-content: flex-start;
      padding: 10px 30px;
      border-top: solid 1px #ddd;
      transition: all ease 0.3s;

      &:hover {
        cursor: pointer;
        background-color: #efefef;
      }

      .avatar {
        width: 60px;
        height: 60px;
        img {
          width: 100%;
          height: -webkit-fill-available;
          display: block;
          border-radius: 100%;
        }
      }
      .descripcion {
        margin-left: 10px;
        h3,
        p {
          margin: 0;
          padding: 0;
        }
      }
    }
  }
}
</style>