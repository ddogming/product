<template>
    <div v-if="isOpen" class="modal-overlay">
        <div class="modal">
        <h2>주문완료</h2>
        <p>주문이 성공적으로 완료되었습니다.</p>
        <button @click="handleClose">확인</button>
    </div>
    </div>
</template>

<script setup>
defineProps({
    isOpen: Boolean
});
const emit = defineEmits(["closeModal"]);
const handleClose = ()=>{
    emit("closeModal",false);
}
</script>

<style lang="scss" scoped>
.modal-overlay{
    border: none;
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0,0,0,0.5);
    display: flex;
    justify-content: center;
    align-items: center;
    .modal{
        background-color: #fff;
        padding: 3rem 5rem;
    }
}
</style>