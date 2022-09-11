<template>
  <!-- vue 개발팁-> 데이터를 어떻게 만들지 부터 먼저 생각 하기 -->
  <!-- 안냥 -->
  <!-- 동적인 UI 만드려면
  0. 디자인해두고
  1. UI의 현재상태를 데이터로 만들어둠
  2. 데이터에 따라 UI 가 어떻게 보일지 작성 (모달창 켜는 스위치) -->

  <!-- props로 자식에게 데이터 보내는 법 -->
  <!-- 1. 밑의 데이터 골라서 보내기
  2. v-bind or : 쓰기
  2-1. ex) 자식:데이터="데이터"
  3. 자식 component 에서 수신받을 코드 작성
  3-1 ex) export default 에 
  props : {
    데이터 이름 : 데이의 형식 Array or Object or Number
  } -->


  <ModalChang :원룸들="원룸들" :누른거="누른거" :모달창열렸니="모달창열렸니"></ModalChang>

  <div class="menu">
    <!-- v-for="작명 in 몇번 반복(숫자)" :key="작명" -->
    <!-- v-for="작명 in 데이터" :key="작명" -->
    <a v-for="a in 메뉴들" :key="a">{{a}}</a>
  </div>


  <!-- <div class="discuont">
    <h4>지금 결제 하면 20% 할인</h4>
  </div> -->
  <!-- --------축약해둔 컴포넌트 쓰는 법--------
  1. vue 파일 import해오고
  2. 컴포넌트에 등록하고
  3. 쓰기 -->
  <!-- 반복적으로 출현할 부분만 컴포넌트 화 권장 -->
  <DiscountPrice></DiscountPrice>

  <!-- <div v-for="(a, i) in 원룸들" :key="i">
    <img :src="a.image" class="room-img">
    <h4 @click="모달창열렸니 = true; 누른거 = i">{{a.title}}</h4>
    <p>{{a.price}}원</p>
  </div> -->

  <!-- 부모가 메세지 수신할 땐 @작명한거="" -->
  <CardList @openModal="모달창열렸니 = true; 누른거 = $event" :원룸="원룸들[i]" v-for="(작명,i) in 원룸들" :key="작명"></CardList>


  
</template>

<script>

// export default 한 것은 자유롭게 작명 가능
// import 작명 from ./경로
import data from './assets/oneroom.js';
import DiscountPrice from './DiscountPrice.vue';
import ModalChang from './ModalChang.vue';
import CardList from './CardList.vue';

export default {
  name: 'App',
  data(){
    return {
      //사용자가 몇 번(number)을 눌렀는지 이기 때문에 숫자가 나음
      누른거 : 0,
      원룸들 : data,
      //데이터를 저장하는 이 공간을 state 라고 부름
      //모달창이 지금 어떻게 보여야 하는지?
      // ex) true 는 열림 flase 는 닫힘
      모달창열렸니 : false,
      신고수 : [0, 0, 0],
      메뉴들 : ['Home', 'Shop', 'About'],
      products : ['역삼동원룸', '천호동원룸', '마포구원룸'],
    }
  },
  //vue 에서 함수 만들고 싶으면 data 바로 밑에다가 methods() 만들어서 거기다가 script 넣어주기
  // methods : {
  //   함수이름(){
  //     this.신고수 += 1;
  //     함수 안에서 데이터 쓸 땐 this.데이터명
  //   }
  // }
  methods : {
    increase(){
      this.신고수 += 1;
    }
  },
  components: {
    // 왼쪽은 언제나 자유작명
    // 왼쪽 오른쪽 이름이 같으면 Discount 이렇게만 써도 됨
    DiscountPrice : DiscountPrice,
    ModalChang : ModalChang,
    CardList : CardList,
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

/* .discount {
  background: #eee;
  padding: 10px;
  margin: 10px;
  border-radius: 5px;
} */

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
