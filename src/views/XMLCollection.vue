<template>
  <div style="padding-left: 20px;padding-top: 20px">
    <div style="display: inline-block; width: 75%;">
      <el-row>
        <div class="title">
          标注工作
        </div>
      </el-row>
      <div class="test-bg">
        <div class="detail_title" id="item1">
          {{title1}}
        </div>
        <div v-html="content1" class="detail_content"></div>
        <div class="detail_title" id="item2">
          {{title3}}
        </div>
        <img src="../assets/img/Border-rec.png" alt="" style="width: 100%; height: 500px; margin-top: 10px; margin-bottom: 10px;"/>
        <div v-html="content3" class="detail_content"></div>
        <div class="detail_title" id="item3">
          {{title2}}
        </div>
        <div v-html="content2" class="detail_content"></div>
        <video
          id="mse"
          autoplay="true"
          playsinline
          controls="controls"
          style="width: 100%; margin-top: 10px; margin-bottom: 10px;"
        >
          <source src="../assets/img/tag_display.mp4" type="video/mp4" />
          你的浏览器不支持Video标签
        </video>
      </div>
      
    </div>
    <div class="side_nav" id="side_test_bar">
      <div :class="whether ? 'isFixed' : ''">
        <h3 class="mb-2" style="margin-bottom: 10px;">内容导航</h3>
        <el-menu
          default-active="1"
          class="el-menu-vertical-demo"
          @open="handleOpen"
          @close="handleClose"
        >
          <el-menu-item index="1" @click="topartern(1)">
            <span>标注工作概述</span>
          </el-menu-item>
          <el-menu-item index="2" @click="topartern(2)">
            <span>标注工作创新</span>
          </el-menu-item>
          <el-menu-item index="3" @click="topartern(3)">
            <span>标注工作演示</span>
          </el-menu-item>
        </el-menu>
      </div> 
    </div>
  </div>
</template>

<script>
import {ref} from 'vue'
import upload from '../views/Upload.vue'

export default {
  name: "XMLCollection",
  components: {upload},
  data() {
    return {
      whether: false,
      form: {
        name: "",
        region: '',
        delivery: false,
        desc: '',
      },
      title1:'标注工作概述',
      content1: '<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;本项目标注工作针对椅子、花盆、广告牌、充电箱四大类作标注工作，训练目标检测模型来检测这四类物体的位置，从而通过三维定位算法进行真实世界定位。</p><p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;标注时，尽可能地使得标注框的边缘与目标物体边缘对齐，在保证标注框语义精确度的情况下，使标注框包含尽可能少的无效背景信息，提高模型的精确度。</p>',
      title2:'标注工作演示',
      content2: '<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;本项目标注工作视频演示如下所示。</p>',
      title3:'标注工作创新',
      content3: '<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;本项目的标注工作对椅子边上的椅子支架进行标注，使椅子支架成为检测椅子的目标。这样做既使得标注框所包含的非目标信息减少，又更加方面确定目标物体的角点，从而目标定位算法可以使用角点去确定目标物体的真实世界坐标。既可以减少背景信息的干扰，又可以方便项目后续对于目标的定位操作。</p>',
    }
  },
  setup() {
    const dialogVisible = ref(false)
    const inputValue = ref('')
    const dynamicTags = ref([])
    const inputVisible = ref(false)
    const circleinput = ref('')
    return {
      dialogVisible,
      inputValue,
      inputVisible,
      dynamicTags,
      circleinput,
      modelselect: 'YOLOX', 
      tableData1: [
        {
          id: "椅子",
          date: "90",
        },
        {
          id: "花盆",
          date: "91",
        },
        {
          id: "广告牌",
          date: "86",
        },
        {
          id: "充电箱",
          date: "92",
        },
      ],
      tableData2: [
        {
          id: "小物体",
          date: "88",
        },
        {
          id: "中物体",
          date: "92",
        },
        {
          id: "大物体",
          date: "96",
        },
        {
          id: "总体精度",
          date: "98",
        },
      ],
      tableData3: [
        {
          id: "标注集1",
          date: " 2022.04.22 16:02",
        },
        {
          id: "标注集2",
          date: " 2022.04.23 16:02",
        },
        {
          id: "标注集3",
          date: " 2022.04.24 16:02",
        },
      ],
    };
  },

  methods: {
    topartern(index) {
      console.log("#item"+index);
      document.querySelector("#item"+index).scrollIntoView({ behavior: "smooth" });
    },
    handleScroll () {
        //计算滚动条位置
      var scrollTop = window.pageYOffset || document.documentElement.scrollTop || document.body.scrollTop;
      //计算绑定div位置
      var offsetTop = document.querySelector('#side_test_bar').offsetTop;
      //进行比较设置位置fixed
      this.whether = scrollTop < offsetTop;
      console.log(this.whether);
    },
    handlecommand(command) {
      this.modelselect = command
      console.log(this.modelselect);
    },
    viewdialog() {
      this.dialogVisible = true
      console.log(this.dialogVisible);
    },
    multi() {
      this.$router.push("/CCTVMulti");
    },
    showInput() {
      this.inputVisible = true
    },
    handleInputConfirm() {
      if (this.inputValue) {
        this.dynamicTags.push(this.inputValue)
      }
      this.inputVisible = false
      this.inputValue = ''
    },
    handleTagClose(index) {
      this.dynamicTags.splice(index, 1)
    },
  },
  mounted() {
    window.addEventListener('scroll', this.handleScroll, true);
  },
  destroyed () {
    window.removeEventListener('scroll', this.handleScroll)
  },
};
</script>

<style scoped>
  #createData :deep(.el-form-item__label) {
    font-size: 16px;
  }
  .form-data {
    background-color: #f8fbf4;
    margin-top: 20px;

    width: 80%;
    padding-top: 50px;
    padding-right: 50px;
    padding-bottom: 30px;
    padding-left: 30px;
  }
  .propset {
    margin-top: 20px;
  }
  .submit-font {
    font-size: 20px;
    margin-bottom: 20px;
  }
  .title {
    height: 50px;
    width: 150px; 
    line-height: 50px;
    font-size: 30px;
    font-family: PingFang SC;
    letter-spacing: 2px;
    font-weight: 700;
    background-color: #f0f0f0;
  }
  .w-20 {
    width: 20%;
  }
  .detail_title {
    font-size: 30px;
    font-weight: 800;
    color: black;
    margin-top: 50px;
    margin-bottom: 20px;
  }
  .detail_content {
    font-size: 22px;
    margin-left: 30px;
    margin-right: 30px;
  }
  .test-bg {
    background-color:#eae9e9;
    margin-left: 50px;
    margin-right: 300px;
    padding: 0px 20px;
    width: 100%;
  }
  .detail_content_sub {
    font-size: 22px;
    margin-left: 30px;
    margin-right: 30px;
    margin-bottom: 30px;
  }
  .side_nav {
    float:right;
    width: 15%;
    margin-top: 50px;
  }
  .isFixed {
    position: fixed;
    top: 200px;
    z-index: 1000;
  }
</style>