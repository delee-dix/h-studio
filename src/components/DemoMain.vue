<template>
  <div class="container">
    <div class="left">
      <h1>Left</h1>
    </div>
    <div class="right">
      <h1>Right</h1>
    </div>
  </div>
  <div class="gnb">
    <button @click="openModal">Button 1</button>
    <button @click="openModal">Button 2</button>
    <button @click="openModal">Button 3</button>
    <button @click="openModal">Button 4</button>
  </div>
</template>

<script>
import { useRouter } from 'vue-router';

export default {
  name: 'DemoMain',
  props: {},
  setup() {
    const router = userRouter();
    const openModal = () => {
      router.push('/');
    }
    return {
      openModal,
    }
  },
}
</script>

<style>
.container {
  display: flex;
  width: 100%;
  height: 90vh;
  /* 화면 전체 높이 */
}

.left {
  flex: 2;
  border: 1px solid;
}

.right {
  flex: 3;
  border: 1px solid;
}

.gnb {
  display: flex;
  width: 100%;
  height: 5vh;
  justify-content: center;
  background-color: lightgray;

  img {
    width: 40px;
    height: 40px;
  }
}
</style>
