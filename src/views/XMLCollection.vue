<template>
  <div style="padding-left: 20px;padding-top: 20px">
    <el-row>
      <div class="title">
        标注工作
      </div>
    </el-row>
    <div class="form-data">
      <img src="../assets/img/Border-rec.png" alt="" style="width: 100%; height: 400px;"/>
      <div class="detail_title">
        {{title}}
      </div>
      <div v-html="content" class="detail_content"></div>
      <el-form v-if="false" id="createData" :model="form" label-width="120px">
        <el-form-item label="标注集名称:">
          <el-input v-model="form.name" />
        </el-form-item>
        <el-form-item label="标注类别:">
          <el-tag
            v-for="(tag, index) in dynamicTags"
            :key="index"
            class="mx-1"
            closable
            :disable-transitions="false"
            @close="handleTagClose(index)"
          >
            {{ tag }}
          </el-tag>
          <el-input
            v-if="inputVisible"
            ref="InputRef"
            v-model="inputValue"
            class="ml-1 w-20"
            size="small"
            @keyup.enter="handleInputConfirm()"
            @blur="handleInputConfirm()"
          />
          <el-button v-else class="button-new-tag ml-1" size="small" @click="showInput()">
            + 新类别
          </el-button>
        </el-form-item>
        <el-form-item label="标注集描述:">
          <el-input v-model="form.desc" type="textarea" />
        </el-form-item>
        <el-form-item label="标注文件上传:">
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
          标注集列表
        </div>
      </el-col>
    </el-row>
    <el-row style="margin-top: 20px">
      <el-table :data="tableData3" stripe border style="width: 100%; font-size: 18px;">
        <el-table-column prop="id" label="训练集名称" width="408">
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
  name: "XMLCollection",
  components: {upload},
  data() {
    return {
      form: {
        name: "",
        region: '',
        delivery: false,
        desc: '',
      },
      title:'特别的标注方式带来更方便快速的定位算法',
      content: '<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;本项目标注工作针对椅子、花盆、广告牌、充电箱四大类作标注工作，训练目标检测模型来检测这四类物体的位置，从而通过三位定位算法进行真实世界定位。</p><p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;本项目的标注工作对椅子边上的椅子支架进行标注，使椅子支架成为检测椅子的目标。这样做既使得标注框所包含的非目标信息减少，又更加方面确定目标物体的角点，从而目标定位算法可以使用角点去确定目标物体的真实世界坐标。既可以减少背景信息的干扰，又可以方便项目后续对于目标的定位操作。</p>',
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
    margin-top: 20px;
    margin-bottom: 20px;
  }
  .detail_content {
    font-size: 22px;
    margin-left: 0px;
    margin-right: 0px;
  }
</style>