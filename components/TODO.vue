<script setup lang="ts">
import { ref } from 'vue'

const props = defineProps({
    msg: {
        default: "TODO",
    }
})

const msg = ref(props.msg)
</script>

<template>
    <div class="abs-b text-center text-3xl color-yellow m-5">
        TODO: {{ msg }}
    </div>
</template>