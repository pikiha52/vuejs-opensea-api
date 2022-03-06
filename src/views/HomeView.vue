<template>
<div class="py-5">
    <CardSlide />
    <Card />
</div>
</template>

<script>
// @ is an alias to /src
import CardSlide from "@/components/CardSlide.vue";
import Card from "@/components/Card.vue";

export default {
  name: "HomeView",
  components: {
    CardSlide,
    Card,
  },
};
</script>
