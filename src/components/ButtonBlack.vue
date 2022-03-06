<template>
    <button class="bg-black hover:bg-transparent hover:border-2 hover:border-black w-auto h-10 px-4 rounded-md hover:text-black text-white font-semibold ">{{ txt }}</button>
</template>


<script>
export default {
    name: 'ButtonBlack',
    props: {
        txt: String,
    },
};
</script>