<template>
  <div class="items-center text-center flex md:flex flex-col">
    <ul v-for="(personaje, index) in listaFavs" :key="index" class="rounded">
      <li
        class="p-3 bg-gray-700 hover:bg-gray-900 hover:scale-105 mb-1 border border-orange-700 rounded"
      >
        <PersonajeFav :favorito="personaje" @eliminarFav="borrarFav" />
      </li>
    </ul>
  </div>
</template>

<script>
import PersonajeFav from "@/components/PersonajeFav.vue";
export default {
  emits: ["eliminarFav"],
  name: "ListaFavs",
  components: {
    PersonajeFav,
  },
  data() {
    return {};
  },
  props: {
    listaFavs: {
      type: Array,
    },
  },
  methods: {
    borrarFav(data) {
      this.$emit("eliminarFav", data);
    },
  },
};
</script>

<style scoped></style>
