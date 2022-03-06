<template>
    <button class="bg-white hover:bg-transparent hover:border-2 hover:border-white w-40 h-10 px-4 rounded-md hover:text-white text-black font-light ">{{ txt }}</button>
</template>


<script>
export default {
    name: 'ButtonPrimary',
    props: {
        txt: String,
    },
};
</script>