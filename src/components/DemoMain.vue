<template>
  <div class="container">
    <div class="left">
      <h1>Left 1</h1>
      <div class="navigation">
        <video ref="leftVideoRef" controls width="60%">
          <source :src="leftVideoSrc" type="video/mp4" />
          <!-- 브라우저에서 지원하지 않을 경우 대체 텍스트 -->
          Your browser does not support the video tag.
        </video>
      </div>
    </div>
    <div class="right" :style="{ backgroundColor: bgColor }">
      <h1>Right 2</h1>
      <div class="content">
        <video ref="rightVideoRef" controls width="100%">
          <source :src="rightVideoSrc" type="video/mp4" />
          <!-- 브라우저에서 지원하지 않을 경우 대체 텍스트 -->
          Your browser does not support the video tag.
        </video>
      </div>
    </div>
  </div>
  <div class="gnb">
    <button @click="toggleModal">Modal Button</button>
    <Modal v-if="isModalOpen" @close="toggleModal"></Modal>
    <button @click="colorChange">Color Change Button</button>
    <button @click="playVideos" :disabled="isDisabled">Video Button</button>
    <button @click="onClick" class="float">Floating Button</button>

  </div>
</template>

<script>
// import { useRouter } from 'vue-router';
import { ref } from 'vue';
import Modal from '../components/DemoModal.vue';
import leftSample from '@/assets/Sample_14s.mp4';
import rightSample from '@/assets/Sample_30s.mp4';

export default {
  name: 'DemoMain',
  components: { Modal },
  props: {},
  setup() {
    // button 1
    const isModalOpen = ref(false);
    const toggleModal = () => {
      isModalOpen.value = !isModalOpen.value;
    }

    // button 2
    const bgColor = ref('#ffffff');
    const colorChange = () => {
      const randomColor = `#${Math.floor(Math.random() * 16777215).toString(16)}`;
      bgColor.value = randomColor;
      alert(`Next color is ${bgColor.value}`);
    }

    // button 3
    const isDisabled = ref(false);
    const leftVideoSrc = ref(leftSample);
    const rightVideoSrc = ref(rightSample);
    const leftVideoRef = ref(null);
    const rightVideoRef = ref(null);
    const playVideos = () => {
      isDisabled.value = true;
      leftVideoRef.value.play();
      rightVideoRef.value.play();
      leftVideoRef.value.addEventListener('ended', handleVideoEnded);
      rightVideoRef.value.addEventListener('ended', handleVideoEnded);
    };

    const handleVideoEnded = () => {
      if (leftVideoRef.value.ended && rightVideoRef.value.ended) {
        isDisabled.value = false;
      }
    };

    // button 4 (모드 실행 버튼)
    const onClick = () => {
      alert('Floating Button Clicked!');
    }

    return {
      isModalOpen,
      isDisabled,
      bgColor,
      leftVideoSrc,
      rightVideoSrc,
      leftVideoRef,
      rightVideoRef,
      playVideos,
      toggleModal,
      colorChange,
      onClick,
    }
  },
}
</script>

<style scoped>
.container {
  display: flex;
  width: 100%;
  height: 93vh;
  /* 화면 전체 높이 */
}

.left {
  flex: 1;
  border: 1px solid;

  .navigation {
    text-align: center;
  }
}

.video {
  border: 1px solid #ccc;
  border-radius: 8px;
  width: 33%;
  height: 100%;
}

.right {
  flex: 2;
  border: 1px solid;
}

.gnb {
  display: flex;
  width: 100%;
  height: 4vh;
  justify-content: center;
  background-color: lightgray;
  border: 1px solid;
  gap: 50px;
}

.float {
  position: fixed;
  bottom: 55px;
  right: 52%;
  width: 200px;
  height: 80px;
  border-radius: 5%;
  border: 1px solid;
  background-color: #E8E8E8;
  color: black;
  font-size: 15px;
  display: flex;
  justify-content: center;
  align-items: center;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.3);
  cursor: pointer;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.float:hover {
  transform: scale(1.1);
  box-shadow: 0 6px 8px rgba(0, 0, 0, 0.4);
}

.float:active {
  transform: scale(0.95);
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.4);
}
</style>
