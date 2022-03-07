<template>
  <!-- This example requires Tailwind CSS v2.0+ -->
  <div class="w-2/5 h-[340px] overflow-y-auto space-y-2 bg-white rounded-md shadow overflow-hidden sm:rounded-md px-2">
  <p class="text-gray-700 font-bold relative">Coint</p>
    <ul role="list" class="divide-y divide-gray-200">
      <div v-for="coints in state.coint" :key="coints.id">
      <li class="flex gap-5 bg-gray-100 rounded-md px-4 py-4 sm:px-6">
        <div class="w-10 rounded-md bg-violet-300 h-10">
          <img :src="coints.image" alt="">
        </div>
        <div class="grid">
          <div class="flex gap-6">
        <p class="text-gray-700 font-semibold text-sm uppercase">{{ coints.symbol }}</p>
        <p class="text-gray-500 font-normal text-xs">Rank {{ coints.market_cap_rank }}</p>
          </div>
        <p class="text-gray-500 font-normal text-xs">{{ coints.market_cap }}</p>
        </div>
      </li>
      </div>
    </ul>
  </div>
</template>

<script>
import { onMounted, reactive } from "vue";
import axios from "../plugins/axios";
import Button from "@/components/Button.vue";
import ButtonBlack from "@/components/ButtonBlack.vue";

export default {
  components: {
    Button,
    ButtonBlack,
  },
  setup() {
    const state = reactive({
      coint: {},
    });

    onMounted(async () => {
      const { data } = await axios.get(
        `https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd&order=market_cap_desc&per_page=10&page=1`
      );
      state.coint = data;
    });

    return {
      state,
    };
  },
};
</script>