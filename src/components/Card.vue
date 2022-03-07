<template>
<div class="bg-white">
  <div class="max-w-2xl py-16 sm:py-24 lg:max-w-7xl">
    <h2 class="text-xl font-bold text-gray-900">NFT List</h2>

    <div class="grid grid-cols-1 gap-y-12 sm:grid-cols-2 sm:gap-x-6 lg:grid-cols-4 xl:gap-x-8">
    <div v-for="nft_assets in state.list.assets" :key="nft_assets.id">
      <div class="bg-gray-100 rounded-md py-4 px-2">
        <div class="relative">
          <div class="relative w-full h-72 rounded-lg overflow-hidden">
            <img :src="nft_assets.image_url" alt="" class="w-full h-full object-center object-cover">
          </div>
          <div class="relative mt-4">
            <h3 class="text-sm font-medium text-gray-900">{{ nft_assets.name }}</h3>
            <p class="mt-1 text-sm text-gray-500">Contract type: {{ nft_assets.asset_contract.asset_contract_type }}</p>
          </div>
          <div class="absolute top-0 inset-x-0 h-72 rounded-lg p-4 flex items-end justify-end overflow-hidden">
            <div aria-hidden="true" class="absolute inset-x-0 bottom-0 h-36 bg-gradient-to-t from-black opacity-50"></div>
            <!-- <p class="relative text-lg font-semibold text-white">$140</p> -->
          </div>
        </div>
        <div class="mt-6 flex justify-center">
          <a :href="nft_assets.permalink">
            <ButtonBlack txt="Show on Open Sea" />
          </a>
        </div>
      </div>
    </div>

    </div>
  </div>
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
      list: {},
    });

    onMounted(async () => {
      const { data } = await axios.get(
        `https://api.opensea.io/api/v1/assets?order_by=pk&order_direction=desc&limit=8&include_orders=true`
      );
      state.list = data;
    });

    return {
      state,
    };
  },
};
</script>