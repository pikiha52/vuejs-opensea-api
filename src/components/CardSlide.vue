<template>
  <div id="app" class="flex overflow-x-auto space-x-40 w-3/4 bg-black rounded-md">
    <div v-for="nft_assets in state.list.assets" :key="nft_assets.id">
      <div class="flex px-4 py-2">
        <div
          class="
            rounded-sm
            w-72
            h-80
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
            <a v-on:click="toggleModal(nft_assets.collection)" type="button">
              <ButtonPrimary txt="View Collection" />
            </a>
          </div>
        </div>
      </div>

    </div>
  </div>

  <div v-if="showModal" class="fixed z-10 inset-0 overflow-y-auto" aria-labelledby="modal-title" role="dialog" aria-modal="true">
  <div class="flex items-end justify-center min-h-screen pt-4 px-4 pb-20 text-center sm:block sm:p-0">
 
    <div class="fixed inset-0 bg-gray-500 bg-opacity-75 transition-opacity" aria-hidden="true"></div>

    <span class="hidden sm:inline-block sm:align-middle sm:h-screen" aria-hidden="true">&#8203;</span>

    <div class="relative inline-block align-bottom bg-white rounded-lg px-4 pt-5 pb-4 text-left overflow-hidden shadow-xl transform transition-all sm:my-8 sm:align-middle sm:max-w-sm sm:w-full sm:p-6">
      <div>
        <div class="mx-auto flex items-center justify-center h-full w-full rounded-full bg-green-100">
         <!-- <img :src="collection.banner_image_url" alt=""> -->
        </div>
        <div class="mt-3 text-center sm:mt-5">
          <h3 class="text-lg leading-6 font-medium text-gray-900" id="modal-title">{{ collectionname }}</h3>
          <div class="mt-2">
            <p class="text-sm text-gray-500">Lorem ipsum dolor sit amet consectetur adipisicing elit. Consequatur amet labore.</p>
          </div>
        </div>
      </div>
      <div class="mt-5 sm:mt-6 flex justify-end">
        <button-black txt="Close" v-on:click="toggleModal()"></button-black>
      </div>
    </div>
  </div>
</div>

</template>



<script>
import { onMounted, reactive } from "vue";
import axios from "../plugins/axios";
import ButtonPrimary from "@/components/Button.vue";
import ButtonBlack from "@/components/ButtonBlack.vue";

export default {
  data() {
    return {
      showModal: false,
      collection: {},
    }
  },
    methods: {
    toggleModal: function(collection){
      this.showModal = !this.showModal;
      return {
        collection,
      }
    }
  },
  components: {
    ButtonPrimary,
    ButtonBlack,
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