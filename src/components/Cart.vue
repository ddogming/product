<template>
    <div class="cart">
        <OpenModal :isOpen="isOpenModal" @closeModal="closeModal"/>
    <div class="cart-list">
        <h2>장바구니</h2>
        <h3 v-if="cart.length === 0">장바구니가 비었습니다</h3>
        <ul v-else>
            <li v-for="list in cart" :key="list.id">
            <img :src="list.image" :alt="list.name">
            <p>{{ list.name }}</p>
            <p>가격:{{ list.price }}</p>
            <p>수량: {{ list.count }}</p>
            <button @click="removeCart(list.id)">삭제</button>
            </li>
        </ul>
    </div>
    <div class="cart-add">
        <h2>주문내역</h2>
        <div class="total">
            <p>상품금액 : {{ totalPrice }}</p>
            <p>배송비 : {{ shoppingFee === 0 ? "무료": `${shoppingFee}원`}}</p>
            <p>(배송비 3,000원 5만원 이상 구매시 무료배송)</p>
            <p>총 결제금액 : {{ payment }}</p>
            <button @click="handleOpen">주문결제</button>
        </div>
    </div>
</div>
</template>

<script setup>
import { computed, ref } from 'vue';
import OpenModal from './OpenModal.vue';
import { useRouter } from 'vue-router';
const isOpenModal = ref(false);
//라우터 인스턴스 생성
const router = useRouter();
const handleOpen = () => {
    isOpenModal.value = true;
}
const closeModal = (value)=>{
    isOpenModal.value = value;
    emit('clear-cart', true);
    router.push('/'); //상품 목록 페이지로 이동
}

const props = defineProps({
    cart : Array
});
const emit = defineEmits(['remove-cart-id', 'clear-cart']);
const removeCart = (cartID) => {
    emit( 'remove-cart-id', cartID );
}
const totalPrice = computed(()=>{
    // let sum = 0;
    // props.cart.forEach((item)=>{
    //     //가격*수량 :
    //     sum += item.price * item.count;
    // });
    // return sum;

    //배열 객체 사용
    let result = props.cart.reduce((sum,item)=>{
        return sum += item.price * item.count;
    },0);
    return result;
});
const shoppingFee = computed(()=>{
    return totalPrice.value >= 50000 ? 0 : 3000;
});
const payment = computed(()=>{
    return totalPrice.value + shoppingFee.value;
});
</script>

<style lang="scss" scoped>
.cart{
    display: flex;
    padding: 2rem 5rem;
    gap: 1rem;
    div{
        flex: 1;
        border: 1px solid #222;
        border-radius: 5px;
    }
    .cart-list{
        ul{
            img{
                width: 200px;
                height: 150px;
                border-radius: 10px;
            }
            li{
                display: flex;
                gap: 1rem;
                align-items: center;
                padding: 1rem;
            }
        }
    }
    .cart-add{
        .total{
            border: none;
            padding: 1rem;
        }
    }
}
</style>