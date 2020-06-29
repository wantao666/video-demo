<template>
  <el-dialog id="createDialog" title="video-demo" width="90%" :visible="true" top="50px">
    <el-container style="height:800px;">
      <el-main style="overflow:hidden;margin-top:-20px;">
        <div class="video">
          <video-player
            class="video"
            ref="videoPlayer"
            :options="playerOptions"
            :playsinline="true"
          ></video-player>
        </div>
        <div class="image">
          <vueCropper
            @mouseenter.native="enter"
            @mouseleave.native="leave"
            ref="cropper"
            :img="uploadImg"
            :outputSize="option.size"
            :outputType="option.outputType"
            :info="true"
            :full="option.full"
            :canMove="option.canMove"
            :canMoveBox="option.canMoveBox"
            :original="option.original"
            :autoCrop="option.autoCrop"
            :fixed="option.fixed"
            :fixedNumber="option.fixedNumber"
            :centerBox="option.centerBox"
            :infoTrue="option.infoTrue"
            :fixedBox="option.fixedBox"
            class="image"
          ></vueCropper>
        </div>
        <div>
          <el-button @click="start()" type="primary">start</el-button>
          <el-button @click="stop()" type="primary">stop</el-button>
        </div>
      </el-main>
    </el-container>
  </el-dialog>
</template>

<script>
export default {
  data() {
    return {
      uploadImg: require("../src/assets/1.jpg"),
      // uploadImg: "",
      uploadVideo: require("../src/assets/test.mp4"),
      option: {
        info: true, // 裁剪框的大小信息
        outputSize: 0.8, // 裁剪生成图片的质量
        outputType: "jpeg", // 裁剪生成图片的格式
        canScale: false, // 图片是否允许滚轮缩放
        autoCrop: false, // 是否默认生成截图框
        fixedBox: false, // 固定截图框大小 不允许改变
        fixed: false, // 是否开启截图框宽高固定比例
        fixedNumber: [7, 5], // 截图框的宽高比例
        full: true, // 是否输出原图比例的截图
        canMove: false, //时候可以移动原图
        canMoveBox: true, // 截图框能否拖动
        original: false, // 上传图片按照原始比例渲染
        centerBox: false, // 截图框是否被限制在图片里面
        infoTrue: true // true 为展示真实输出图片宽高 false 展示看到的截图框宽高
      },
      playerOptions: {
        muted: true,
        language: "en",
        autoplay: true,
        playbackRates: [0.7, 1.0, 1.5, 2.0],
        sources: [
          {
            type: "video/mp4",
            src: require("../src/assets/test.mp4")
          }
        ],
        controlBar: {}
      }
    };
  },
  methods: {
    enter() {
      this.$refs.cropper.startCrop();
    },
    leave() {
      // this.$refs.cropper.clearCrop();
    },
    start() {
      console.log(this.player);
    },
    stop() {}
  },
  computed: {
    player() {
      return this.$refs.videoPlayer.player;
    }
  }
};
</script>

<style scoped>
#createDialog /deep/ .image {
  background-image: none;
  width: 500px;
  height: 600px;
  opacity: 0.8;
  /* position: absoulute;
  left: -500px; */
}
#createDialog /deep/ .video {
  float: left;
}
#createDialog /deep/ .vjs_video_3-dimensions {
  width: 500px;
  height: 600px;
}
</style>