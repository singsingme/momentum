<template>
  <!-- 안냥 -->
  <!-- 동적인 UI 만드려면
  0. 디자인해두고
  1. UI의 현재상태를 데이터로 만들어둠
  2. 데이터에 따라 UI 가 어떻게 보일지 작성 (모달창 켜는 스위치) -->
  <div class="black-bg" v-if="모달창열렸니 == true">
    <div class="white-bg">
      <img :src="원룸들[누른거].image" style="whidth:100%">
      <h4>{{원룸들[누른거].title}}</h4>
      <p>{{원룸들[누른거].content}}</p>
      <p>{{원룸들[누른거].price}} 원</p>
      <button @click="모달창열렸니 = false">닫기</button>
    </div>
  </div>

  <div class="menu">
    <!-- v-for="작명 in 몇번 반복(숫자)" :key="작명" -->
    <!-- v-for="작명 in 데이터" :key="작명" -->
    <a v-for="작명 in 메뉴들" :key="작명">Home</a>
  </div>



  <!-- HTML 태그안의 속성 데이터 바인딩은 :어쩌구
  HTML 태그안의 내용 데이터 바인딩은 {{어쩌구}} -->
  <div v-for="(작명, i) in 원룸들" :key="i">
    <img :src="원룸들[i].image" class="room-img">
    <h4 @click="모달창열렸니 = true; 누른거 = i">{{원룸들[i].title}}</h4>
    <p>{{원룸들[i].price}}원</p>
  </div>

  
</template>

<script>
// export default 한 것은 자유롭게 작명 가능
import data from './assets/oneroom.js';


export default {
  name: 'App',
  data(){
    return {
      //사용자가 몇 번(numgber)을 눌렀는지 이기 때문에 숫자가 나음
      누른거 : 0,
      원룸들 : data,
      //데이터를 저장하는 이 공간을 state 라고 부름
      //모달창이 지금 어떻게 보여야 하는지?
      // ex) true 는 열림 flase 는 닫힘
      모달창열렸니 : true,
      신고수 : [0, 0, 0],
      메뉴들 : ['Home', 'Shop', 'About'],
      products : ['역삼동원룸', '천로동원룸', '마포구원룸'],
    }
  },
  methods : {
    increase(){
      this.신고수 += 1;
    }
  },
  components: {

  }
}
</script>

<style>

body {
  margin : 0;
}
div {
  box-sizing: border-box;
}
.black-bg {
  width: 100%; height:100%;
  background: rgba(0,0,0,0.5);
  position: fixed; padding: 20px;
}
.white-bg {
  width: 100%; background: white;
  border-radius: 8px;
  padding: 20px;
} 

.room-img {
  width: 100%;
  margin-top: 40px;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.menu {
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}
.menu a {
  color: white;
  padding: 10px;
}
</style>
