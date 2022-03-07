<template>
<div class="flex">
    <CardSlide />
    <CardList />
</div>
    <Card />
</template>

<script>
// @ is an alias to /src
import CardSlide from "@/components/CardSlide.vue";
import Card from "@/components/Card.vue";
import CardList from '@/components/CardList.vue';

export default {
  name: "HomeView",
  components: {
    CardSlide,
    Card,
    CardList,
  },
};
</script>
