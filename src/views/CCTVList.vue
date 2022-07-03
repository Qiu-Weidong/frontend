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
        <!-- <el-button @click="upload">上传视频</el-button> -->
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
      <el-table :data="tableData" style="width: 100%">
        <el-table-column prop="date" label="日期" width="180">
        </el-table-column>
        <el-table-column prop="time" label="时间" width="180"></el-table-column>
        <el-table-column prop="camera" label="所属摄像头" width="180">
        </el-table-column>

        <el-table-column prop="id" label="物体id" width="180">
        </el-table-column>
        <el-table-column prop="address1" label="移动前坐标/米" width="180">
        </el-table-column>
        <el-table-column prop="address2" label="移动后坐标/米">
        </el-table-column>
      </el-table>
    </el-row>
  </div>
</template>

<script>
import {ref} from 'vue';

export default {
  name: "CCTVList",
  setup() {
    const dialogVisible = ref(false);

    return {
      value: "",
      dialogVisible,
      tableData: [
        {
          date: "2022-5-10",
          time: "20:35",
          id: "椅子_1",
          address1: "(123,456,0)",
          address2: "(123, 123,0)",
          camera: "摄像头1",
        },
        {
          date: "2022-4-17",
          time: "20:35",
          id: "广告牌_2",
          address1: "(12,13,0)",
          address2: "(17, 23, 0)",
          camera: "摄像头4",
        },
        {
          date: "2022-3-12",
          time: "20:35",
          id: "椅子_1",
          address1: "(14, 231, 89)",
          address2: "(132,32,56)",
          camera: "摄像头2",
        },
        {
          date: "2022-1-1",
          time: "20:35",
          id: "椅子_4",
          address1: "(14, 98, 45)",
          address2: "(92, 91, 78)",
          camera: "摄像头1",
        },
        {
          date: "2022-1-1",
          time: "20:35",
          id: "花盆_3",
          address1: "(14, 98, 45)",
          address2: "(92, 91, 78)",
          camera: "摄像头1",
        },
        {
          date: "2022-1-1",
          time: "20:35",
          id: "花盆_1",
          address1: "(14, 98, 45)",
          address2: "(92, 91, 78)",
          camera: "摄像头1",
        },
        {
          date: "2022-1-1",
          time: "20:35",
          id: "椅子_4",
          address1: "(14, 98, 45)",
          address2: "(92, 91, 78)",
          camera: "摄像头1",
        },
        {
          date: "2022-1-1",
          time: "20:35",
          id: "广告牌_5",
          address1: "(14, 98, 45)",
          address2: "(92, 91, 78)",
          camera: "摄像头1",
        },
        {
          date: "2022-1-1",
          time: "20:35",
          id: "椅子_4",
          address1: "(14, 98, 45)",
          address2: "(92, 91, 78)",
          camera: "摄像头1",
        },
        {
          date: "2022-1-1",
          time: "20:35",
          id: "充电桩_2",
          address1: "(14, 98, 45)",
          address2: "(92, 91, 78)",
          camera: "摄像头1",
        },
        {
          date: "2022-6-17",
          time: "17:15",
          id: "消防栓_6",
          address1: "(14, 98, 45)",
          address2: "(92, 91, 78)",
          camera: "摄像头1",
        },
        {
          date: "2022-6-30",
          time: "19:05",
          id: "广告牌_2",
          address1: "(14, 98, 45)",
          address2: "(92, 91, 78)",
          camera: "摄像头1",
        },
        {
          date: "2022-7-3",
          time: "09:31",
          id: "椅子_1",
          address1: "(14, 98, 45)",
          address2: "(92, 91, 78)",
          camera: "摄像头1",
        },
        {
          date: "2022-7-4",
          time: "00:35",
          id: "椅子_3",
          address1: "(14, 98, 45)",
          address2: "(92, 91, 78)",
          camera: "摄像头1",
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