<template>
  <div style="padding-left: 20px;padding-top: 20px">
    <el-row>
      <div class="title">
        训练新的模型
      </div>
      <el-button type="primary" round style="height:30px;margin-top: 5px; margin-left: 10px;" @click="dialogVisible = true">训练数据设置</el-button>
      <el-button type="info" round style="height:30px;margin-top: 5px; margin-left: 10px;">当前模型详情</el-button>
    </el-row>
    <el-row>
      <el-col :span="6">
        <div style="width: 200px; margin-top: 15px; font-size: 22px; font-weight: 600">
          模型训练结果
        </div>
      </el-col>
    </el-row>
    <el-row style="margin-top: 20px;">
      <el-table :data="tableData1" stripe border style="width: 50%; font-size: 18px;">
        <el-table-column prop="id" label="类别" width="345">
        </el-table-column>
        <el-table-column prop="date" label="精度（AP）" width="345">
        </el-table-column>
      </el-table>
      <el-table :data="tableData2" stripe border style="width: 50%; font-size: 18px;">
        <el-table-column prop="id" label="类别" width="345">
        </el-table-column>
        <el-table-column prop="date" label="精度（AP）" width="345">
        </el-table-column>
      </el-table>
    </el-row>
    <!-- <el-row>
      <el-col :span="6">
        <el-select v-model="value" placeholder="请选择摄像头">
          <el-option
            v-for="item in options"
            :key="item.value"
            :label="item.label"
            :value="item.value"
          >
          </el-option>
        </el-select>
      </el-col>
       <el-col :span="6">
        <el-button @click="multi">分频显示</el-button>
      </el-col>
    </el-row> -->

    <!-- <el-row>
      <el-image style="width: 100%" :src="url" fit="contain"></el-image>
    </el-row> -->

    <!-- <el-row v-if="multi" >
        <el-image style="width: 50%" :src="url" fit="contain"></el-image>
        <el-image style="width: 50%" :src="url" fit="contain"></el-image>
    </el-row> -->
    <el-row>
      <el-col :span="6">
        <div style="width: 200px; margin-top: 15px; font-size: 22px; font-weight: 600">
          训练模型列表
        </div>
      </el-col>
    </el-row>
    <el-row style="margin-top: 20px">
      <el-table :data="tableData3" stripe border style="width: 100%; font-size: 18px;">
        <el-table-column prop="id" label="模型名称" width="408">
        </el-table-column>
        <el-table-column prop="date" label="训练开始日期" width="408">
        </el-table-column>
        <el-table-column prop="timeuse" label="训练时长" width="410">
        </el-table-column>
        <el-table-column label="模型操作" width="170">
          <el-button type="success" icon="el-icon-check" circle title="选用"></el-button>
          <el-button type="info" icon="el-icon-info" circle title="详情"></el-button>
          <el-button type="danger" icon="el-icon-delete" circle title="删除"></el-button>
        </el-table-column>
      </el-table>
    </el-row>
    <!-- <el-row>
      <el-button>更多</el-button>
    </el-row> -->
    <el-dialog
      v-model="dialogVisible"
      title="训练集设置"
      width="30%"
    >
      <div class="submit-font">训练图片集</div>
      <upload style="margin-bottom: 20px;"/>
      <div class="submit-font">训练标注文件（xml格式）</div>
      <upload style="margin-bottom: 20px;"/>
      <div class="submit-font">参数设置</div>
      <div>
        <div class="propset">
          类别设置：
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
        </div>
        <div class="propset">
          训练周期设置：
          <el-input v-model="circleinput" placeholder="请输入周期" clearable style="width: 50%;"></el-input>
        </div>
        <div class="propset">
          预训练模型选择：
          <el-dropdown @command="handlecommand">
            <el-button type="primary">
              {{modelselect}}&nbsp;&nbsp;<i class="el-icon-bottom"></i>
            </el-button>
            <template #dropdown>
              <el-dropdown-menu>
                <el-dropdown-item command="YOLOX">YOLOX</el-dropdown-item>
                <el-dropdown-item command="BorderDet">BorderDet</el-dropdown-item>
              </el-dropdown-menu>
            </template>
          </el-dropdown>
        </div>
      </div>
      <template #footer>
        <span>
          <el-button @click="dialogVisible = false">取 消</el-button>
          <el-button type="primary" @click="dialogVisible = false">确 定</el-button>
        </span>
      </template>
    </el-dialog>
  </div>
</template>

<script>
import {ref} from 'vue'
import upload from '../views/Upload.vue'

export default {
  name: "NewModel",
  components: {upload},
  setup() {
    const dialogVisible = ref(true)
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
  .propset {
    margin-top: 20px;
  }
  .submit-font {
    font-size: 20px;
    margin-bottom: 20px;
  }
  .title {
    height: 50px;
    width: 200px; 
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
</style>