<script setup>
const emits = defineEmits(['addTimer'])

</script>


<template>
    <div class="wrapper" @click="() => emits('addTimer')">
        <div class="add_btn"></div>
    </div>
</template>


<style scoped>
.wrapper {
    align-self: flex-start;
    width: 225px;
    height: 120px;
    background: var(--bg-color);
    display: flex;
    justify-content: center;
    align-items: center;
    flex-shrink: 0;
}

.wrapper:hover {
    cursor: pointer;
    opacity: 0.8;

}

.add_btn {
    width: 3px;
    height: 20px;
    position: relative;
    background: var(--off-color);
}

.add_btn::after {
    content: '';
    position: absolute;
    width: 20px;
    height: 3px;
    top: 9px;
    left: -9px;
    background: var(--off-color);
}

</style>