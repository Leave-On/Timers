<script setup>
import { ref } from 'vue';

const isRunning = ref(false)
const seconds = ref(0)
const minutes = ref(0)
const hours = ref(0)

let interval

const onToggleStart = () => {
    if (!isRunning.value) {
        isRunning.value = true
        interval = setInterval(() => {
            seconds.value++
            if (seconds.value > 59) {
                seconds.value = 0
                minutes.value++
            }
            if (minutes.value > 59) {
                minutes.value = 0
                hours.value++
            }


        }, 1000)
    } else {
        isRunning.value = false
        clearInterval(interval)
    }
}

const onReset = () => {
    clearInterval(interval)
    isRunning.value = false
    seconds.value = 0
    minutes.value = 0
    hours.value = 0
}


</script>

<template>
    <div class="wrapper">
        <div class="output" :class="{isActive: isRunning}">
            <span v-if="hours > 0">{{ hours }}:</span>
            <span v-if="minutes > 0 || hours > 0">
                <span v-if="hours > 0">0</span><span>{{ minutes }}:</span>
            </span>
            <span v-if="(minutes > 0 || hours > 0) && seconds < 10">0</span><span>{{
                seconds }}</span>
        </div>
        <div class="divider" :class="{isActive: isRunning}"></div>
        <div class="btns" :class="{isActive: isRunning}">
            <div class="left_btns">
                <div v-if="!isRunning" class="start_btn" @click="onToggleStart"></div>
                <div v-if="isRunning" class="pause_btn" @click="onToggleStart">
                    <div class="pause_btn_inner"></div>
                </div>
            </div>
            <div class="reset_btn">
                <div class="reset_btn_inner"  :class="{isActive: isRunning}" @click="onReset"></div>
            </div>
        </div>
    </div>
</template>


<style scoped>


.wrapper {
    width: 225px;
    height: 118px;
    background: var(--bg-color);
    color: var(--off-color);
    align-self: start;
    text-align: center;
}

.divider {
    width: 100%;
    height: 0;
    border: 1px solid var(--off-color);
}

.output {
    width: 100%;
    height: 50%;
    color: var(--off-color);
    background: inherit;
    display: flex;
    justify-content: center;
    align-items: center;
}

.btns {
    width: 100%;
    height: 50%;
    background: inherit;
    display: flex;
    justify-content: center;
    align-items: center;
}

.left_btns {
    position: relative;
    width: 50%;
    height: 100%;
    background: inherit;
}

.start_btn {
    position: absolute;
    bottom: 20px;
    left: 70px;
    border: 10px solid var(--bg-color);
    border-right: 0;
    border-left: 17px solid var(--off-color);
}

.pause_btn {
    position: absolute;
    bottom: 20px;
    left: 70px;
    width: 17px;
    height: 20px;
    background: transparent;
}

.pause_btn_inner {
    background: var(--on-color);
    width: 3px;
    height: 20px;
    position: absolute;
    left: 3px;
}

.pause_btn_inner::after {
    content: '';
    background: var(--on-color);
    width: 3px;
    height: 20px;
    position: absolute;
    left: 7px;
}

.reset_btn {
    background: inherit;
    width: 50%;
    height: 100%;
}
.reset_btn_inner {
    position: absolute;
    background: var(--off-color);
    width: 20px;
    height: 20px;
    bottom: 20px;
    right: 70px;
}

/* .reset_btn::after {
    content: '';
    position: absolute;
    background: var(--off-color);
    width: 20px;
    height: 20px;
    bottom: 20px;
    right: 70px;
} */


.start_btn:hover,
.pause_btn:hover,
.reset_btn_inner:hover {
    cursor: pointer;
    opacity: 0.8;
}

.isActive {
    color: var(--on-color);
    border-color: var(--on-color);
    transition: all 0.3s ease;
}
.reset_btn_inner.isActive {
    background: var(--on-color);
    transition: all 0.3s ease;
}
</style>