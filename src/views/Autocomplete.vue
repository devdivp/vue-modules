<template>
  <div class="about flex flex-col items-center">
    <div class="absolute inset-0 z-0" @click="modal = false"></div>
    <!-- <input
      type="text"
      name="autocomplete"
      class="bg-blue-300 px-4 py-2 z-10"
      autocomplete="off"
      id="autocomplete"
      v-model="typing"
      @input="filterStatesMethod"
      @focus="modal = true"
    /> -->
    <input
      type="text"
      name="autocomplete"
      class="bg-blue-300 px-4 py-2 z-10"
      autocomplete="off"
      id="autocomplete"
      v-model="typing"
      @focus="modal = true"
    />

    <div v-if="filteredStates && modal" class="z-10">
      <ul class="w-48 bg-gray-800 text-white">
        <li
          v-for="(filteredState, index) in filteredStates"
          :key="index"
          class="py-2 border-b cursor-pointer"
          @click="setState(filteredState)"
        >
          {{ filteredState }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      typing: "",

      states: ["Alabama", "Florida", "Alaska", "Texas"],

      filteredStates: [],

      modal: false,
    };
  },

  mounted: function () {
    this.filterStatesMethod();
  },

  methods: {
    filterStatesMethod() {
      if (this.typing.length == 0) {
        this.filteredStates = this.states;
      }

      this.filteredStates = this.states.filter((state) => {
        return state.toLowerCase().startsWith(this.typing.toLowerCase());
      });
    },

    setState(state) {
      this.typing = state;
      this.modal = false;
    },
  },

  watch: {
    typing() {
      this.filterStatesMethod();
    },
  },
};
</script>