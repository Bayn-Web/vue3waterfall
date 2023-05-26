<template>
    <div class="card">
        <div v-waterfall class="card-item" v-for="(item, index) in  cardData " :key="index"
            :style="{ background: item.color, height: item.height }">
            <p class="text">{{ item.id }}</p>
        </div>
    </div>
</template>
<script setup lang="ts">
import { reactive } from "vue"
const { cardData, columnHeights } = reactive<{
    cardData: {
        id: number;
        color: string;
        height: string;
    }[];
    columnHeights: number[];
}>({
    cardData: [
        { id: 1, color: '#76da6e', height: '100px' },
        { id: 2, color: '#57c797', height: '80px' },
        { id: 3, color: '#54cac7', height: '70px' },
        { id: 4, color: '#b16dc7', height: '120px' },
        { id: 5, color: '#dc933d', height: '130px' },
        { id: 6, color: '#b74acf', height: '90px' },
        { id: 7, color: '#d93e5a', height: '80px' },
        { id: 8, color: '#5474dd', height: '100px' },
        { id: 9, color: '#e42526', height: '120px' },
        { id: 10, color: '#e86c92', height: '90px' },
    ],
    columnHeights: [0, 0, 0]
})
const vWaterfall = {
    mounted(el: HTMLDivElement) {
        updateLayout(el)
    }
}

const updateLayout = (item: HTMLDivElement) => {
    const column = getMinColumnHeights(columnHeights)
    const itemTop = columnHeights[column]
    const itemLeft = column * item.clientWidth;
    item.style.transform = `translate(${itemLeft}px, ${itemTop}px)`
    columnHeights[column] += item.offsetHeight
    console.log(columnHeights)
}

const getMinColumnHeights = (arr: any) => {
    let min = Math.min(...arr)
    return arr.indexOf(min) !== -1 ? arr.indexOf(min) : 0
}
</script>
<style scoped>
.card {
    position: relative;

}

.card-item {
    width: 200px;
    text-align: center;
    color: #ffffff;
    display: flex;
    justify-content: center;
    align-items: center;
    position: absolute;
    top: 0;
    left: 0;
}
</style>