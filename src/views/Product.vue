<template>
  <div class="flex flex-col items-center">
    <div class="absolute inset-0 z-0" @click="modal = false"></div>
    <label for="Products" class="font-bold">Select Product</label>
    <input
      type="text"
      name="autocomplete"
      class="bg-blue-300 px-4 py-2 z-10"
      autocomplete="off"
      id="autocomplete"
      v-model="typing"
      @focus="modal = true"
    />

    <div v-if="filteredProducts && modal" class="z-10">
      <ul class="w-48 bg-gray-800 text-white">
        <li
          v-for="(filteredProduct, index) in filteredProducts"
          :key="index"
          class="py-2 border-b cursor-pointer"
          @click="setProduct(filteredProduct)"
        >
          {{ filteredProduct }}
        </li>
      </ul>
    </div>

    <ProductPricing class="z-10 mt-20" :typing="typing"></ProductPricing>
  </div>
</template>

<script>
import ProductPricing from "../components/ProductPricing.vue";

export default {
  components: {
    ProductPricing,
  },

  data: function () {
    return {
      typing: "",

      products: ["Mercury", "Earth", "Venus", "Mars"],

      filteredProducts: [],

      modal: false,
    };
  },

  mounted: function () {
    this.filterProductsMethod();
  },

  methods: {
    filterProductsMethod() {
      if (this.typing.length == 0) {
        this.filteredProducts = this.products;
      }

      this.filteredProducts = this.products.filter((product) => {
        return product.toLowerCase().startsWith(this.typing.toLowerCase());
      });
    },

    setProduct(product) {
      this.typing = product;
      this.modal = false;
    },
  },

  watch: {
    typing() {
      this.filterProductsMethod();
    },
  },
};
</script>