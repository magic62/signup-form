<script setup>

const props = defineProps({
    text: String,
    status: Boolean
})

</script>

<template>
    <li v-if="!status" class="text-red-500"><b>{{ text }}</b></li>
</template>