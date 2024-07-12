<template>
  <div class="h-100 d-flex align-center justify-space-between">
    <!-- 👉 Footer: left content -->
    <span class="d-flex align-center">
      &copy;
      {{ new Date().getFullYear() }}
      <!-- Made With
      <VIcon
        icon="ri-heart-line"
        color="error"
        size="1.25rem"
        class="mx-1"
      /> -->
      By <a
        href="https://www.vectoranalytics.io/"
        target="_blank"
        rel="noopener noreferrer"
        class="text-primary ms-1"
      >vectoranalytics</a>
    </span>
    <!-- 👉 Footer: right content -->
    <span class="d-md-flex gap-x-4 text-primary d-none">
      <a
        href="https://www.vectoranalytics.io/privacy-policy"
        target="noopener noreferrer"
      >Terms and Conditions</a>

    </span>
  </div>
</template>
