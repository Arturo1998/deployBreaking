<template>
  <div
    class="m-auto bg-gradient-to-b from-gray-900 via-gray-800 to-amber-900 min-h-screen"
  >
    <img
      src="./assets/imagenFondo.jpg"
      alt=""
      class="min-w-100 max-h-96 mx-auto"
    />
    <div class="mt-5 mb-5">
      <Buscador @buscarPersonaje="filtrar" v-model="filtro" />
    </div>

    <div class="text-center flex flex-col lg:flex-row w-100">
      <div class="m-auto" v-if="filtrarPersonajes">
        <h1
          class="mb-2 rounded-lg bg-gray-600 text-white border border-orange-700 p-2"
        >
          Tu búsqueda
        </h1>
        <ListaPersonajes
          :lista="filtrarPersonajes"
          @enviarFav="aniadirFavorito"
          bg-gray-80
        />
      </div>
      <div
        class="border-orange-700 rounded p-50 text-center m-auto mt-1 mb-10"
        v-if="this.favs.length > 0"
      >
        <h1
          class="mb-5 rounded-lg bg-gray-600 text-white border border-orange-700 p-2"
        >
          Lista de favoritos
        </h1>
        <ListaFavs :listaFavs="favs" @eliminarFav="eliminarElemento" />
      </div>
    </div>
    <loading v-model:active="isLoading" :is-full-page="true" loader="bars" />
  </div>
</template>

<script>
import Loading from "vue-loading-overlay";
import "vue-loading-overlay/dist/css/index.css";
import axios from "axios";
import Buscador from "@/components/Buscador.vue";
import ListaPersonajes from "@/components/ListaPersonajes.vue";
import ListaFavs from "@/components/ListaFavs.vue";
export default {
  name: "App",
  components: {
    ListaPersonajes,
    ListaFavs,
    Buscador,
    Loading,
  },

  data() {
    return {
      characters: [],
      favs: [],
      filtrar_por: "",
      filtro: "",
      isLoading: false,
    };
  },

  mounted() {
    if (localStorage.getItem("favs")) {
      this.favs = JSON.parse(localStorage.getItem("favs"));
    }

    this.loadCharacters();
  },

  computed: {
    filtrarPersonajes() {
      if (this.filtrar_por != "") {
        return this.characters.filter((character) =>
          character.name.toUpperCase().includes(this.filtrar_por.toUpperCase())
        );
      } else {
        return null;
      }
    },
  },

  methods: {
    async loadCharacters() {
      try {
        const response = await axios.get(
          `https://www.breakingbadapi.com/api/characters`
        );
        this.characters = response.data;
      } catch (error) {
        console.log(error);
      }
    },

    aniadirFavorito(data) {
      const result = this.favs.filter(
        (personaje) => personaje.char_id === data.char_id
      );
      if (result.length === 0) {
        this.favs.push(data);
        this.guardarLocal();
      }
    },

    eliminarElemento(data) {
      this.favs = this.favs.filter((el) => el !== data);
      localStorage.setItem("favs", JSON.stringify(this.favs));
    },

    filtrar(data) {
      this.filtrar_por = data;
      this.isLoading = true;
      setTimeout(() => {
        this.isLoading = false;
      }, 1500);
    },

    guardarLocal() {
      const parsed = JSON.stringify(this.favs);
      localStorage.setItem("favs", parsed);
    },
  },
};
</script>

<style scoped></style>
