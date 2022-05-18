<template>
  <div>
    <!-- <video id="mse" autoplay="true" playsinline controls="controls" style="width:100%">
      <source
        src="http://html5videoplayer.net/videos/madagascar3.mp4"
        type="video/mp4"
      />
      你的浏览器不支持Video标签
    </video> -->
    <video id="mse" autoplay="true" playsinline controls="controls" style="width:100%">
      <source
        src="../assets/img/video.mp4"
        type="video/mp4"
      />
      你的浏览器不支持Video标签
    </video>
  </div>
</template>

<script>
export default {
  name: "VideoTest",
  setup() {
    return {};
  },
};
</script>
