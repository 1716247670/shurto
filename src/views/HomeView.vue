<script setup>
let level = 5;
let count = 1;
let correctArray = generateArray(level);
let uniqueArray = generateUniqueArray(level);

console.log(uniqueArray);
function generateUniqueArray(level = 5) {
    let arr = generateArray(level)
    // 使用 Fisher-Yates Shuffle 算法随机排序数组
    for (let i = arr.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [arr[i], arr[j]] = [arr[j], arr[i]];
    }

    let result = [];
    for (let i = 0; i < level; i++) {
        result.push(arr.slice(i * level, (i + 1) * level));
    }
    return result;
}
function generateArray(level = 5) {
    let arr = [];
    for (let i = 1; i <= level ** 2; i++) {
        arr.push(i);
    }
    return arr;
}
function getValue(value, event) {
    if (value === count) {
        event.target.style.backgroundColor = 'green';
        count++;
    }
}
</script>

<template>
    <main>
        <div class="box">
            <div class="row" v-for="(row, key) in uniqueArray">
                <div class="cell" v-for="(item, key) in row" @click="getValue(item, $event)">
                    {{ item }}
                </div>
            </div>
        </div>
    </main>
</template>

<style scoped>
.box {
    display: flex;
    flex-wrap: wrap;
}

.box .row {
    background-color: #f0f0f0;
}

.box .row .cell {
    margin: 10px;
    border-radius: 5px;
    width: 5vw;
    height: 5vw;
    border: 1px solid #000;
    text-align: center;
    line-height: 5vw;
    cursor: pointer;
}

.box .row .cell:hover {
    background-color: rgba(255, 0, 0, 0.8);
    color: #f0f0f0;
}
</style>