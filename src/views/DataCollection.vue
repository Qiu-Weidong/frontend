<template>
  <div style="padding-left: 20px;padding-top: 20px">
    <div style="display: inline-block; width: 75%;">
      <el-row>
        <div class="title">
          数据采集
        </div>
      </el-row>
      <!-- <div v-if="false" class="form-data">
        <el-steps direction="vertical" :active="step_num" align-center>
          <el-step title="Step 1" description="视频抽帧处理" @click="change1()"/>
          <el-step title="Step 2" description="图像数据增强" @click="change2()"/>
          <el-step title="Step 3" description="人工图像去重" @click="change3()"/>
        </el-steps>
      </div> -->
      <div class="test-bg">
        <div id="item1">
          <div class="detail_title">
            {{title1}}
          </div>
          <div v-html="content1" class="detail_content"></div>
        </div>
        <div id="item2">
          <div class="detail_title">
            {{title3}}
          </div>
          <div v-html="content3" class="detail_content"></div>
          <div class="detail_content_sub">
            <p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;人工图像去重的示例如下图所示。</p>
            <img src="../assets/img/人工去重.png" alt="" style="width: 100%; height: 500px; margin-top: 10px; margin-bottom: 10px;"/>
          </div>
        </div>
        <div id="item3">
          <div class="detail_title">
            {{title2}}
          </div>
          <div v-html="content2" class="detail_content"></div>
          <div class="detail_content_sub">
            <p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;考虑到现有的大多数算法自带对于图像数据的某些数据增强方法，如通过裁剪、缩放的形式对原始图像数据集进行扩充，以使得训练模型能够应对遮挡条件和距离不一条件下的目标检测任务。所以本项目对于原始图像的数据增强偏向于图像色彩方面的数据增强。</p>
            <p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;对比度是指图像中颜色之间的区别，通过修改对比度可以达到的效果如图所示。</p>
            <img src="../assets/img/对比度增强.png" alt="" style="width: 100%; height: 500px; margin-top: 10px; margin-bottom: 10px;"/>
            <p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;亮度就是指图像中光线的强弱程度，亮度越高图像越耀眼。通过修改亮度可以达到的效果如图所示。</p>
            <img src="../assets/img/亮度增强.png" alt="" style="width: 100%; height: 500px; margin-top: 10px; margin-bottom: 10px;"/>
            <p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;色度本文中特指图像中色彩的亮度，通过改变色度可以达到的图像数据增强的效果如所示。</p>
            <img src="../assets/img/色度增强.png" alt="" style="width: 100%; height: 500px; margin-top: 10px; margin-bottom: 10px;"/>
          </div>
        </div>
      </div>
      <div v-if="false" class="form-data">
        <el-form id="createData" :model="form" label-width="120px">
          <el-form-item label="图像集名称:">
            <el-input v-model="form.name" />
          </el-form-item>
          <el-form-item label="数据集描述:">
            <el-input v-model="form.desc" type="textarea" />
          </el-form-item>
          <el-form-item label="图像上传:">
            <upload style="margin-bottom: 20px;"/>
          </el-form-item>
          <el-form-item>
            <el-button type="primary" @click="onSubmit">提交</el-button>
            <el-button>取消</el-button>
          </el-form-item>
        </el-form>
      </div>
      <el-row v-if="false">
        <el-col :span="6">
          <div style="width: 200px; margin-top: 20px; font-size: 22px; font-weight: 600">
            图像集列表
          </div>
        </el-col>
      </el-row>
      <el-row v-if="false" style="margin-top: 20px">
        <el-table :data="tableData3" stripe border style="width: 100%; font-size: 18px;">
          <el-table-column prop="id" label="图像集名称" width="408">
          </el-table-column>
          <el-table-column prop="date" label="建立日期" width="408">
          </el-table-column>
          <el-table-column label="模型操作" width="170">
            <el-button type="success" icon="el-icon-check" circle title="选用"></el-button>
            <el-button type="info" icon="el-icon-info" circle title="详情"></el-button>
            <el-button type="danger" icon="el-icon-delete" circle title="删除"></el-button>
          </el-table-column>
        </el-table>
      </el-row>
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
            <span>视频抽帧处理</span>
          </el-menu-item>
          <el-menu-item index="2" @click="topartern(2)">
            <span>人工图像去重</span>
          </el-menu-item>
          <el-menu-item index="3" @click="topartern(3)">
            <span>图像数据增强</span>
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
  name: "DataCollection",
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
      step_num: 1,
      title1:'视频抽帧处理',
      content1: '<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;由于极短的时间内目标运动幅度较小，保留视频原本帧数会大大增加目标检测模型的复杂度，故本项目首先对实地单目摄像头提取的视频数据进行抽帧处理。</p><p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;抽帧处理过后的视频，再对视频按帧切分为图像集合，由此获得约5000余张原始图像。</p>',
      title2:'图像数据增强',
      content2: '<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;为了使得训练出来的目标检测模型能够应对大多数环境条件（光照条件、遮挡条件等）下的检测任务，对原始数据集的图像进行了亮度、对比度、色度上的随机增强，同时添加目标物体被遮挡的图像样本，提高模型泛化性。由此获得数据增强集合。',
      title3:'人工图像去重',
      content3: '<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;图像中相似的目标物体位置与目标遮挡关系对于训练出来的目标检测模型带来的作用也是相近的，本项目对数据增强集进行了人工图像去重，即把上述相近的图像保留一张作为训练样本。获得最终的模型图像训练集合，约1600余张图像。</p>',
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
    change1() {
      this.step_num = 1;
    },
    change2() {
      this.step_num = 2;
    },
    change3() {
      this.step_num = 3;
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