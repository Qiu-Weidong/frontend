<template>
  <div>
    <el-row>
      <el-col :span="6">
        <el-date-picker v-model="value" type="date" placeholder="选择日期">
        </el-date-picker>
      </el-col>
      <el-col :span="6">
        <el-button>下载所有表单</el-button>
      </el-col>
      <el-col :span="6">
        <el-button @click="upload">上传视频</el-button>
        <el-dialog v-model="dialogVisible" width="30%">
          <el-upload
            style="margin-left: 20px"
            class="upload-demo"
            drag
            action="http://jsonplaceholder.typicode.com/api/posts/"
            multiple
          >
            <i class="el-icon-upload"></i>
            <div class="el-upload__text">
              将文件拖到此处，或
              <em>点击上传</em>
            </div>
            <!-- <template #tip>
                    <div class="el-upload__tip">上传图片的zip压缩包</div>
                </template> -->
          </el-upload>
        </el-dialog>
      </el-col>
    </el-row>
    <el-row>
      <el-table :data="tableData" stripe style="width: 100%">
        <el-table-column prop="date" label="日期" width="“240”">
        </el-table-column>
        <el-table-column prop="time" label="时间" width="“240”">
        </el-table-column>
        <el-table-column prop="camera" label="所属摄像机" width="“240”">
        </el-table-column>
        <!-- <el-table-column prop="address2" label="移动之后坐标" width="“240”">
        </el-table-column> -->

        <el-table-column fixed="right" label="操作" width="120">
          <!-- <template slot-scope="scope"> -->
          <el-button type="text" size="small" @click="detail"> 详情 </el-button>
          <!-- </template> -->
        </el-table-column>
      </el-table>
    </el-row>
  </div>
</template>

<script>
import {ref} from 'vue';

export default {
  name: "VideoList",
  setup() {
    const dialogVisible = ref(false);

    return {
      value: "",
      dialogVisible,
      tableData: [
        {
          time: "19:48",
          date: "2022-5-11",
          camera: '摄像机1'
          
        },
        {
          time: "19:48",
          date: "2022-5-11",
          camera: '摄像机2'
          
        },
        {
          time: "19:48",
          date: "2022-5-11",
          camera: '摄像机3'
          
        },
        {
          time: "19:48",
          date: "2022-5-11",
          camera: '摄像机2'
          
        },
        {
          time: "19:48",
          date: "2022-5-11",
          camera: '摄像机5'
          
        },
        {
          time: "19:48",
          date: "2022-5-11",
          camera: '摄像机6'
          
        },
        {
          time: "19:48",
          date: "2022-5-11",
          camera: '摄像机1'
          
        },
        {
          time: "椅子_1",
          date: "2022-5-11",
          camera: '摄像机3'
          
        },
      ],
    };
  },

  methods: {
    detail() {
      this.$router.push("videodetail");
    },
    upload() {
      console.log('上传视频');
      this.dialogVisible = true;
    }
  },
};
</script>

<style>
</style>