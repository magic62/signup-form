<script setup>
const value = defineModel('value')

const props = defineProps({
    name: String,
    type: String
})
</script>

<template>
    <div class="flex flex-col">
        <label :for="name.replace(/\s+/g, '-').toLowerCase()"><b>{{ name }}</b></label>
        <input :id="name.replace(/\s+/g, '-').toLowerCase()" :type=type
            class="border-2 border-black w-56 text-black p-1 mb-1" v-model="value">
        <div class="w-56">
            <slot></slot>
        </div>
    </div>
</template>