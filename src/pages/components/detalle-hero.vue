<template>
  <div>
    <div v-if="loading" class="loadingClase">Cargando datos...</div>
    <div class="visor" v-if="elemento.length == null">
      <div class="header">
        <h3>Detalle</h3>
        <button @click="elemento = []">Cerrar</button>
      </div>
      <div class="hero">
        <div class="cover">
          <img width="100%" :src="elemento.avatarURL" alt="" />
          <h3>{{ elemento.nombre }}</h3>
          <small>{{ elemento.nombreReal }}</small>
          <ul class="habilidades">
            <li v-for="(habilidad, idh) in elemento.habilidades" :key="idh">{{ habilidad }}</li>
          </ul>
        </div>
        <div class="desc">
          <p>{{ elemento.descripcion }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "detalle-hero",
  props: {
    elemento: {
      type:[ Array, Object]
    },
    loading: {
      type: Boolean,
    },
  },
};
</script>

<style lang="scss">
.loadingClase {
  background-color: #fff;
  margin-top: 10px;
  border: solid 1px #ddd;
  padding: 20px;
  text-align: center;
}
.visor {
  background-color: #fff;
  border: solid 1px #ddd;
  border-radius: 3px;
  margin-top: 20px;
  .header {
    display: flex;
    align-items: center;
    flex-direction: row;
    justify-content: space-between;
    margin-bottom: 5px;
    background-color: #f0f0f0;
    padding: 10px;
    border-bottom: solid 1px #ddd;

    h3 {
      margin: 0;
    }
  }

  .hero {
    padding: 10px 30px;
    text-align: center;

    .cover {
      img {
        border-radius: 100%;
        width: 100px;
        height: 100px;
        margin-bottom: 10px;
      }
      h3 {
        margin: 0;
      }
      small {
        font-size: 12px;
      }

      .habilidades {
        list-style: none;
        margin: 0;
        padding: 0;
        display: flex;
        align-items: stretch;
        justify-content: stretch;
        flex-direction: row;
        flex-wrap: wrap;
        li {
          font-size: 10px;
          padding: 10px;
          background-color: #f44336;
          color: #fff;
          margin: 5px;
          border-radius: 14px;
          padding: 4px 10px;
        }
      }
    }

    .desc {
      border-top: solid 1px #ddd;
      margin-top: 10px;
      p {
        font-size: 14px;
        color: #666;
        text-align: justify;
      }
    }
  }
}
</style>