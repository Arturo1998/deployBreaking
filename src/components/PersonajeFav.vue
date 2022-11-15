<template>
  <div class="items-center text-center flex flex-col w-40">
    <img
      class="rounded-full max-h-32"
      :src="favorito.img"
      alt=""
      v-if="verMas"
    />
    <h1 class="text-white p-3 text-xl">{{ favorito.name }}</h1>
    <div v-if="!verMas" class="text-white mb-3">
      <h1 class="text-orange-500">Dead or alive: </h1>
      <p >{{ favorito.status }}</p>
      <h1 class="text-orange-500">Interpretado por: </h1>
      <p >{{ favorito.portrayed }}</p>
    </div>
    <div class="flex flex-col">
      <button
        class="rounded-lg text-white bg-orange-700 p-2 w-20 mb-2"
        @click="mostrarinfo"
      >
        {{ botonInfo }}
      </button>
      <button
        class="rounded-lg text-white bg-red-800 p-2 mb-2"
        @click="eliminarFav"
      >
        🗑️
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "PersonajeFav",
  components: {},
  data() {
    return {
      verMas: true,
      botonInfo: "Ver más",
    };
  },
  props: {
    favorito: {
      type: Object,
    },
  },
  emits: ["eliminarFav"],
  methods: {
    eliminarFav() {
      if (confirm(`¿Estás seguro de eliminar a ${this.favorito.name}?`))
        this.$emit("eliminarFav", this.favorito);
    },

    mostrarinfo() {
      this.verMas = !this.verMas;
      if (this.verMas === false) {
        this.botonInfo = "Ver menos";
      } else {
        this.botonInfo = "Ver más";
      }
    },
  },
};
</script>

<style scoped></style>
