<template>
  <div style="padding-left: 20px;padding-top: 20px">
    <el-row>
      <div class="title">
        数据采集
      </div>
    </el-row>
    <div class="form-data">
      <el-steps :active="step_num" align-center>
        <el-step title="Step 1" description="视频抽帧处理" @click="change1()"/>
        <el-step title="Step 2" description="图像数据增强" @click="change2()"/>
        <el-step title="Step 3" description="人工图像去重" @click="change3()"/>
      </el-steps>
      <div v-show="step_num == 1">
        <div class="detail_title">
          {{title1}}
        </div>
        <div v-html="content1" class="detail_content"></div>
      </div>
      <div v-show="step_num == 2">
        <div class="detail_title">
          {{title2}}
        </div>
        <div v-html="content2" class="detail_content"></div>
      </div>
      <div v-show="step_num == 3">
        <div class="detail_title">
          {{title3}}
        </div>
        <div v-html="content3" class="detail_content"></div>
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
    <el-row>
      <el-col :span="6">
        <div style="width: 200px; margin-top: 20px; font-size: 22px; font-weight: 600">
          图像集列表
        </div>
      </el-col>
    </el-row>
    <el-row style="margin-top: 20px">
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
</template>

<script>
import {ref} from 'vue'
import upload from '../views/Upload.vue'

export default {
  name: "DataCollection",
  components: {upload},
  data() {
    return {
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
      content2: '<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;为了使得训练出来的目标检测模型能够应对大多数环境条件（光照条件、遮挡条件等）下的检测任务，对原始数据集的图像进行了亮度、对比度、色度上的随机增强，同时添加目标物体被遮挡的图像样本，提高模型泛化性。由此获得数据增强集合',
      title3:'人工图像去重',
      content3: '<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;图像中相似的目标物体位置与目标遮挡关系对于训练出来的目标检测模型带来的作用也是相近的，本项目对数据增强集进行了人工图像去重，即把上述相近的图像保留一张作为训练样本。获得最终的模型图像训练集合，约3300余张图像。</p>',
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
      options: [
        {
          value: "选项1",
          label: "摄像机1",
        },
        {
          value: "选项2",
          label: "摄像机2",
        },
        
      ],
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
          id: "模型1",
          date: " 2022.04.22 16:02",
          timeuse: "1h",
        },
        {
          id: "模型2",
          date: " 2022.04.23 16:02",
          timeuse: "2h",
        },
        {
          id: "模型3",
          date: " 2022.04.24 16:02",
          timeuse: "3h",
        },
      ],
    };
  },

  methods: {
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
    text-align: center;
    font-size: 30px;
    font-weight: 800;
    color: black;
    margin-top: 50px;
    margin-bottom: 20px;
  }
  .detail_content {
    font-size: 22px;
    margin-left: 80px;
    margin-right: 80px;
    margin-bottom: 20px;
  }
</style>