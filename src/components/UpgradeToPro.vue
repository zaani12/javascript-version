<template>
  <!-- Upload Button -->
  <div class="upload-button-container">
    <button @click="redirectToUpload" class="upload-button">
      Upload
      <span class="button-inner" />
    </button>
  </div>
</template>

<script setup>
import { useRouter } from 'vue-router'

const router = useRouter()

const redirectToUpload = () => {
  router.push('/wizard') // Adjust the path to the correct route in your application
}
</script>

<style lang="scss" scoped>
.upload-button,
.button-inner {
  display: inline-flex;
  box-sizing: border-box;
  align-items: start;
  justify-content: start;
  border: 0;
  border-radius: 6px;
  margin: 0;
  animation: anime 12s linear infinite;
  appearance: none;
  background: linear-gradient(-45deg, #ffa63d, #ff3d77, #338aff, #3cf0c5);
  background-size: 600%;
  color: rgba(255, 255, 255, 90%);
  cursor: pointer;
  font-size: 0.9375rem;
  font-weight: 500;
  letter-spacing: 0.43px;
  line-height: 1.2;
  min-inline-size: 50px;
  outline: 0;
  padding-block: 0.625rem;
  padding-inline: 1.25rem;
  text-decoration: none;
  text-transform: none;
  vertical-align: middle;
}

.upload-button-container {
  position: fixed;
  bottom: 5%;
  left: 50%;
  transform: translateX(-50%);
  z-index: 999;
}

.upload-button {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  border: 0;
  border-radius: 6px;
  background: linear-gradient(-45deg, #ffa63d, #ff3d77, #338aff, #3cf0c5);
  background-size: 600%;
  color: rgba(255, 255, 255, 90%);
  cursor: pointer;
  font-size: 0.9375rem;
  font-weight: 500;
  letter-spacing: 0.43px;
  line-height: 1.2;
  padding-block: 0.625rem;
  padding-inline: 1.25rem;
  text-decoration: none;
  animation: anime 12s linear infinite;

  &:hover {
    color: white;
    text-decoration: none;
  }

  .button-inner {
    position: absolute;
    z-index: -1;
    filter: blur(12px);
    inset: 0;
    opacity: 0;
    transition: opacity 200ms ease-in-out;
  }

  &:not(:hover) .button-inner {
    opacity: 0.8;
  }
}

@keyframes anime {
  0% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
  100% {
    background-position: 0% 50%;
  }
}
</style>
