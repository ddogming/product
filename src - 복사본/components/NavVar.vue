<template>
    <nav>
        <h1>햄부가티</h1>
        <ul>
            <li v-for="(list,idx) in categories" :key="idx" @click="selectedClick(list)">
            {{ list }}
        </li>   
        </ul>
    </nav>
</template>

<script setup>
import { categories } from '../assets/products';

defineProps({
    categories : Array
});
const emit = defineEmits(['selected']);
const selectedClick = (list) =>{
    emit('selected',list);
}
</script>

<style scoped>
    nav{
        display: flex;
        justify-content: space-between;
        padding: 2rem 5rem;
        ul{
            display: flex;
            gap: 3rem;
            li{
                cursor: pointer;
                &:hover{
                    font-weight: bolder;
                    color: blue;
                }
            }
        }
    }
</style>