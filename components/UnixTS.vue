<template>
    {{ currentTS }}
</template>

<script>
export default {
    data() {
        return {
            currentTS: new Date().valueOf()
        };
    },
    mounted() {
        this.intervalId = setInterval(() => {
            this.currentTS = new Date().valueOf();
        }, 137);
    },
    unmounted() {
        clearInterval(this.intervalId);
    }
};
</script>