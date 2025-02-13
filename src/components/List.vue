<template>
    <div class="products-list">
        <div class="card" v-for="list in products" :key="list.id">
            <img :src="list.image" :alt="list.name">
            <p>{{list.name}} /{{ list.price }}won</p>
            <button @click="addToList(list)">장바구니 추가</button>
        </div>
    </div>
</template>

<script setup>
    defineProps({
        products:Array,
    });
    const emit = defineEmits(['add-to-cart']);
    const addToList = (list)=>{
        emit('add-to-cart', list );
    }
</script>

<style lang="scss" scoped>
.products-list{
    display: flex;
    flex-wrap: wrap;
    gap: 2rem;
    justify-content: center;
    p{
        margin-left: -7px;
        font-weight: bolder;
        font-size: 20px
    }
    button{
        margin-left: -100px;
        padding: 5px;
        border-radius: 5px;
        cursor: pointer;
    }
    button:hover{
        background-color: yellow;
    }
    .card{
        width: 200px;
        text-align: center;
        margin: 95px;
        // margin-left: -0.7px;
        img{
            width: 350px;
            height: 250px;
            object-fit: cover;
            border-radius: 10px;
        }
    }
}
</style>