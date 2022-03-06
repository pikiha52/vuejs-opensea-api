<template>
  <div class="flex overflow-x-auto space-x-40 w-3/4 bg-black rounded-md">
    <div v-for="nft_assets in state.list.assets" :key="nft_assets.id">
      <div class="flex px-4 py-2">
        <div
          class="
            rounded-sm
            w-72
            h-56
            flex
            justify-center
            items-center
            bg-gradient-to-r
            from-blue-200
            to-pink-200
          "
        >
          <img
            :src="nft_assets.image_url"
            class="w-56 h-56 rounded-full"
            alt=""
          />
        </div>
        <div class="px-4">
          <p class="text-white font-bold mb-2">{{ nft_assets.name }}</p>
          <div class="flex items-center gap-2 py-5">
            <img v-if="nft_assets.creator !== null"
              :src="nft_assets.creator.profile_img_url"
              class="w-8 h-8 rounded-full"
              alt=""
            />
            <div v-if="nft_assets.creator !== null">
              <p class="text-white font-normal text-sm">
                {{ nft_assets.creator.user.username }}
              </p>
            </div>
            <div v-else>
              <p class="text-white font-normal text-sm">Not Creator</p>
            </div>
          </div>
          <!-- <p class="text-gray-300 text-xs">Price NFT</p> -->
          <div class="flex gap-6">
            <ButtonPrimary txt="View Open Sea" />
            <ButtonPrimary txt="View Collection" />
          </div>
        </div>
      </div>
    </div>
    <!-- <div v-for="nft_list in state.list.assets" :key="nft_list.id">
        as
    </div> -->
  </div>
</template>

<script>
import { onMounted, reactive } from "vue";
import axios from "../plugins/axios";
import ButtonPrimary from "@/components/Button.vue";

export default {
  components: {
    ButtonPrimary,
  },
  setup() {
    const state = reactive({
      list: {},
    });

    onMounted(async () => {
      const { data } = await axios.get(
        `https://api.opensea.io/api/v1/assets?order_by=pk&order_direction=desc&limit=10&include_orders=true`
      );
      state.list = data;
    });

    return {
      state,
    };
  },
};
</script>