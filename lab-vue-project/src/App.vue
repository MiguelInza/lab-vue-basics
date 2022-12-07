<template>
  <div>
    <article v-for="(item, index) of topItems" :key="item.uuid" class="flex">
      <div>{{ index }}</div>
      <div>{{ aMayusculas(item) }}</div>
      <img :src="item.image" :alt="item.name" width="96" />
      {{ item.price }}
      <input type="number" v-model="item.quantity" placeholder="0" />
      {{ item.quantity * item.price }}
    </article>
  </div>

  <div v-if="!limitReached">Añade mínimo 3 artículos</div>

  <div v-else-if="items.length < 5">
    Añade 5 articulos mas para envio gratuio
  </div>

  <button v-else>
    Confirmar compra
    {{ numberOfItems }}
  </button>
</template>

<script>
import ITEMS from "./items.json";
export default {
  data() {
    return {
      items: ITEMS,
      mostrar: false,
    };
  },

  computed: {
    topItems() {
      return this.items.slice(0, 5);
    },
    numberOfItems() {
      return this.topItems.length;
    },
    limitReached() {
      return this.items.length > 3;
    },
  },

  methods: {
    aMayusculas(item) {
      return item.name.toUpperCase();
    },
    mostrarTres(top) {
      const tres = this.items.slice(0, top);
      return tres;
    },
  },
};
</script>

<style>
.flex {
  display: flex;
  justify-content: space-around;
}
</style>




