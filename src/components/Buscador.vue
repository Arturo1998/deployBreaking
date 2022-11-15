<template>
  <div class="text-center">
    <input
      type="text"
      v-model="filtro"
      placeholder="Busca un personaje"
      class="w-56 bg-transparent border border-orange-600 text-white mr-1 py-1 px-2 rounded-full"
      @keyup.enter="buscarPersonaje"
    />
  </div>
</template>

<script>
export default {
  name: "Buscador",
  emits: ["buscarPersonaje"],
  components: {},
  data() {
    return {
      filtro: "",
    };
  },

  methods: {
    buscarPersonaje() {
      this.$emit("buscarPersonaje", this.filtro);
    },
  },
};
</script>

<style scoped></style>
