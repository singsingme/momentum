<template>
    <div>
        <img :src="원룸.image" class="room-img">
        <!-- 부모에게메세지 보낼땐 $emit('작명', 데이터) -->
        <h4 @click="clickModal"> {{원룸.title}} </h4>
        <p>{{원룸.price}} 원</p>
    </div>
</template>


<script>
export default {
    name : 'CardList',
    props : {
        원룸 : Object,
    },
    methods : {
        clickModal(){
            // 데이터 함수안에서 참조할때는 this 꼭 붙이기
            // props든 data든 $변수든 밑에서 쓸 땐 this 붙이기
            this.$emit('openModal', this.원룸.id)
        }
    },
}
</script>

<style>

</style>