<template>
  <div class="mt-6">
    <input
      type="text"
      class="w-96 text-2xl bg-gray-300 p-3 rounded-lg focus:outline-none"
      :placeholder="template"
      v-model="number"
    />
  </div>
</template>

<script>
export default {
  props: ["template"],

  data: function () {
    return {
      number: "",
      format: "",
      regex: "^",
    };
  },

  mounted() {
    let x = 1;

    this.format = this.template.replace(/X+/g, () => "$" + x++);

    this.template.match(/X+/g).forEach((char) => {
      this.regex += "(\\d{" + char.length + "})?";
    });
  },

  watch: {
    number() {
      this.number = this.number
        .replace(/[^0-9]/g, "")
        // .replace(/^(\d{3})?(\d{3})?(\d{4})?/g, this.format)
        .replace(new RegExp(this.regex, "g"), this.format)
        .substr(0, this.template.length);
    },
  },
};
</script>