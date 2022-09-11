<template>
<!-- Modal 은 App.vue의 자식 component임 -->
<!-- {{데이터바인딩}}은 밑에 데이터가 있어야 가능함 -->
  <!-- ------------모달창------------ -->
  <div class="black-bg" v-if="모달창열렸니 == true">
    <div class="white-bg">
      <!-- HTML 태그안의 속성 데이터 바인딩은 :어쩌구
      HTML 태그안의 내용 데이터 바인딩은 {{어쩌구}} -->
      <!-- []안에 들어갈 데이터가 몇번 째 인지 하드코딩해야 되기 때문에 data에 누른거 라는 데이터를 만들어 줌 -->
      <img :src="원룸들[누른거].image" style="whidth:100%">
      <h4>{{원룸들[누른거].title}}</h4>
      <p>{{원룸들[누른거].content}}</p>
      <p> {{month}}개월 선택함 : {{원룸들[누른거].price * month}} 원</p>
      <input v-model="month">
      <button @click="$emit('closeModal')">닫기</button>
    </div>
  </div>
</template>

<script>
export default {
    name : 'ModalChang',
    data(){
      return {
        month : 1,
      }
    },
    props : {
      원룸들 : Array,
      누른거 : Number,
      모달창열렸니 : Boolean,
    }
}
</script>

<style>

</style>