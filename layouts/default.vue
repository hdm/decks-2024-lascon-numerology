<!-- default.vue -->
<template>
    <div class="slidev-layout default">
        <slot />
    </div>
    <div class="abs-br p-1 mb-2 mr-3 flex gap-2 opacity-75">
        <img src="/runzero.svg" width="100px">
    </div>
    <div class="abs-bl mb-4 ml-3 text-xs opacity-30">
        <SlideCurrentNo /> /
        <SlidesTotal />
    </div>
</template>