<template>
  <div class="mt-6 mb-10">
    <ul v-for="(personaje, index) in lista" :key="index" class="">
      <li class="mb-5 max-w-xl hover:scale-105">
        <Personaje
          :personaje="personaje"
          @enviarFav="aniadirElementoFavorito"
        />
      </li>
    </ul>
  </div>
</template>

<script>
import Personaje from "@/components/Personaje.vue";
export default {
  name: "ListaPersonajes",
  emits: ["enviarFav"],
  components: {
    Personaje,
  },
  data() {
    return {
      filtro: "",
    };
  },
  props: {
    lista: {
      type: Array,
    },
  },

  methods: {
    aniadirElementoFavorito(data) {
      this.$emit("enviarFav", data);
      console.log("recibiendo en segundo nivel...");
    },
  },
};
</script>

<style scoped></style>
