<template>
  <div
    class="w-1/2 rounded-lg shadow px-6 py-10 flex flex-col items-center"
    :class="productDetails[typing.toLowerCase()].bgcolor"
    v-if="productDetails[typing.toLowerCase()]"
  >
    <h1 class="uppercase text-4xl text-white font-bold pb-2">{{ typing }}</h1>
    <div class="bg-gray-400 rounded-full flex justify-around p-1">
      <button
        v-for="(price, frequency) in productDetails[typing.toLowerCase()]
          .plans[0].pricing"
        :key="frequency"
        @click="currentFrequency = frequency"
        class="rounded-full text-xs font-bold px-6 py-1 uppercase focus:outline-none"
        :class="
          currentFrequency == frequency ? 'bg-blue-600 text-gray-200' : ''
        "
      >
        {{ frequency }}
      </button>
    </div>

    <div class="flex w-full pt-8">
      <div
        v-for="plan in productDetails[typing.toLowerCase()].plans"
        :key="plan.plan_id"
        class="w-1/2 text-white"
      >
        <h1 class="text-2xl font-bold" v-text="plan.name"></h1>

        <ul class="pt-4">
          <li
            v-for="(benefit, index) in plan.benefits[currentFrequency]"
            :key="index"
            v-text="benefit"
          ></li>
        </ul>

        <div class="flex justify-center pt-8">
          <div class="text-4xl font-bold">
            {{ getPrice(plan.pricing[currentFrequency].price) }}
          </div>
          <div class="pl-1 pt-2 text-gray-300">
            {{ plan.pricing[currentFrequency].label }}
          </div>
        </div>
      </div>
    </div>

    <div class="pt-4 text-center text-gray-400 text-sm font-bold">
      <a href="#" @click.prevent="currency = 'usd'">USD</a> |
      <a href="#" @click.prevent="currency = 'inr'">INR</a> |
      <a href="#" @click.prevent="currency = 'eur'">EUR</a>
    </div>
  </div>
</template>

<script>
export default {
  props: ["typing"],

  methods: {
    getPrice(price) {
      return this["currency" + this.currency.toUpperCase()](price);
    },

    currencyUSD(price) {
      return "$" + price;
    },

    currencyINR(price) {
      return "₹ " + Math.ceil(price * 73.45);
    },

    currencyEUR(price) {
      return Math.ceil(price * 0.85) + "€";
    },

    resetData() {
      return Object.assign(this.$data, this.$options.data.apply(this));
    },
  },

  watch: {
    typing: function () {
      if (this.productDetails[this.typing.toLowerCase()]) {
        this.resetData();
      }
    },
  },

  data: function () {
    return {
      currentFrequency: "monthly",
      currency: "usd",

      productDetails: {
        mercury: {
          bgcolor: "bg-blue-900",
          plans: [
            {
              plan_id: 1,
              name: "Starter",
              benefits: {
                monthly: ["Benefit 1", "Benefit 2", "Benefit 3", "Benefit 4"],
                yearly: [
                  "Benefit 1",
                  "Benefit 2",
                  "Benefit 3",
                  "Benefit 4",
                  "Benefit 5",
                  "Benefit 6",
                ],
                lifetime: [
                  "Benefit 1",
                  "Benefit 2",
                  "Benefit 3",
                  "Benefit 4",
                  "Benefit 5",
                  "Benefit 6",
                  "Benefit 7",
                  "Benefit 8",
                ],
              },
              pricing: {
                monthly: { price: 99, label: "/mo" },
                yearly: { price: 499, label: "/yr" },
                lifetime: { price: 1200, label: "" },
              },
            },
            {
              plan_id: 2,
              name: "Pro",
              benefits: {
                monthly: ["Benefit 1", "Benefit 2", "Benefit 3", "Benefit 4"],
                yearly: [
                  "Benefit 1",
                  "Benefit 2",
                  "Benefit 3",
                  "Benefit 4",
                  "Benefit 5",
                  "Benefit 6",
                ],
                lifetime: [
                  "Benefit 1",
                  "Benefit 2",
                  "Benefit 3",
                  "Benefit 4",
                  "Benefit 5",
                  "Benefit 6",
                  "Benefit 7",
                  "Benefit 8",
                ],
              },
              pricing: {
                monthly: { price: 199, label: "/mo" },
                yearly: { price: 999, label: "/yr" },
                lifetime: { price: 2200, label: "" },
              },
            },
          ],
        },
        earth: {
          bgcolor: "bg-green-900",
          plans: [
            {
              plan_id: 1,
              name: "Starter",
              benefits: {
                monthly: ["Benefit 1", "Benefit 2", "Benefit 3", "Benefit 4"],
                yearly: [
                  "Benefit 1",
                  "Benefit 2",
                  "Benefit 3",
                  "Benefit 4",
                  "Benefit 5",
                  "Benefit 6",
                ],
                lifetime: [
                  "Benefit 1",
                  "Benefit 2",
                  "Benefit 3",
                  "Benefit 4",
                  "Benefit 5",
                  "Benefit 6",
                  "Benefit 7",
                  "Benefit 8",
                ],
              },
              pricing: {
                monthly: { price: 99, label: "/mo" },
                yearly: { price: 499, label: "/yr" },
                lifetime: { price: 1200, label: "" },
              },
            },
            {
              plan_id: 2,
              name: "Pro",
              benefits: {
                monthly: ["Benefit 1", "Benefit 2", "Benefit 3", "Benefit 4"],
                yearly: [
                  "Benefit 1",
                  "Benefit 2",
                  "Benefit 3",
                  "Benefit 4",
                  "Benefit 5",
                  "Benefit 6",
                ],
                lifetime: [
                  "Benefit 1",
                  "Benefit 2",
                  "Benefit 3",
                  "Benefit 4",
                  "Benefit 5",
                  "Benefit 6",
                  "Benefit 7",
                  "Benefit 8",
                ],
              },
              pricing: {
                monthly: { price: 199, label: "/mo" },
                yearly: { price: 999, label: "/yr" },
                lifetime: { price: 2200, label: "" },
              },
            },
          ],
        },
        venus: {
          bgcolor: "bg-orange-900",
          plans: [
            {
              plan_id: 1,
              name: "Starter",
              benefits: {
                monthly: ["Benefit 1", "Benefit 2", "Benefit 3", "Benefit 4"],
                yearly: [
                  "Benefit 1",
                  "Benefit 2",
                  "Benefit 3",
                  "Benefit 4",
                  "Benefit 5",
                  "Benefit 6",
                ],
                lifetime: [
                  "Benefit 1",
                  "Benefit 2",
                  "Benefit 3",
                  "Benefit 4",
                  "Benefit 5",
                  "Benefit 6",
                  "Benefit 7",
                  "Benefit 8",
                ],
              },
              pricing: {
                monthly: { price: 99, label: "/mo" },
                yearly: { price: 499, label: "/yr" },
                lifetime: { price: 1200, label: "" },
              },
            },
            {
              plan_id: 2,
              name: "Pro",
              benefits: {
                monthly: ["Benefit 1", "Benefit 2", "Benefit 3", "Benefit 4"],
                yearly: [
                  "Benefit 1",
                  "Benefit 2",
                  "Benefit 3",
                  "Benefit 4",
                  "Benefit 5",
                  "Benefit 6",
                ],
                lifetime: [
                  "Benefit 1",
                  "Benefit 2",
                  "Benefit 3",
                  "Benefit 4",
                  "Benefit 5",
                  "Benefit 6",
                  "Benefit 7",
                  "Benefit 8",
                ],
              },
              pricing: {
                monthly: { price: 199, label: "/mo" },
                yearly: { price: 999, label: "/yr" },
                lifetime: { price: 2200, label: "" },
              },
            },
          ],
        },
        mars: {
          bgcolor: "bg-black",
          plans: [
            {
              plan_id: 1,
              name: "Starter",
              benefits: {
                monthly: ["Benefit 1", "Benefit 2", "Benefit 3", "Benefit 4"],
                yearly: [
                  "Benefit 1",
                  "Benefit 2",
                  "Benefit 3",
                  "Benefit 4",
                  "Benefit 5",
                  "Benefit 6",
                ],
                lifetime: [
                  "Benefit 1",
                  "Benefit 2",
                  "Benefit 3",
                  "Benefit 4",
                  "Benefit 5",
                  "Benefit 6",
                  "Benefit 7",
                  "Benefit 8",
                ],
              },
              pricing: {
                monthly: { price: 99, label: "/mo" },
                yearly: { price: 499, label: "/yr" },
                lifetime: { price: 1200, label: "" },
              },
            },
            {
              plan_id: 2,
              name: "Pro",
              benefits: {
                monthly: ["Benefit 1", "Benefit 2", "Benefit 3", "Benefit 4"],
                yearly: [
                  "Benefit 1",
                  "Benefit 2",
                  "Benefit 3",
                  "Benefit 4",
                  "Benefit 5",
                  "Benefit 6",
                ],
                lifetime: [
                  "Benefit 1",
                  "Benefit 2",
                  "Benefit 3",
                  "Benefit 4",
                  "Benefit 5",
                  "Benefit 6",
                  "Benefit 7",
                  "Benefit 8",
                ],
              },
              pricing: {
                monthly: { price: 199, label: "/mo" },
                yearly: { price: 999, label: "/yr" },
                lifetime: { price: 2200, label: "" },
              },
            },
          ],
        },
      },
    };
  },
};
</script>