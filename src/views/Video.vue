<template>
  <div>
    <el-row>
    <el-button @click="upload">上传视频</el-button>
    <el-dialog v-model="dialogVisible" width="30%">
      <el-upload style="margin-left: 20px;" class="upload-demo" drag action="http://jsonplaceholder.typicode.com/api/posts/" multiple>
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
    </el-row>

    <el-row>
      <video id="mse" autoplay="true" playsinline controls="controls" style="width:100%">
      <source
        src="../assets/img/video.mp4"
        type="video/mp4"
      />
      你的浏览器不支持Video标签
    </video>
    </el-row>

    <!-- <el-row v-if="multi" >
        <el-image style="width: 50%" :src="url" fit="contain"></el-image>
        <el-image style="width: 50%" :src="url" fit="contain"></el-image>
    </el-row> -->

    <el-row>
      <el-table :data="tableData" style="width: 100%">
        <el-table-column prop="date" label="日期" width="240">
        </el-table-column>
        <el-table-column prop="id" label="物体id" width="240">
        </el-table-column>
        <el-table-column prop="address1" label="移动前坐标" width="240">
        </el-table-column>
        <el-table-column prop="address2" label="移动后坐标"> </el-table-column>
      </el-table>
    </el-row>
    <!-- <el-row>
      <el-button>更多</el-button>
    </el-row> -->
  </div>
</template>

<script>
import {ref} from 'vue'

export default {
  name: "Video",
  setup() {
    const dialogVisible = ref(false);

    return {
      dialogVisible,
      url: "https://cdn.jsdelivr.net/gh/Qiu-Weidong/pictures/images/毕设/微信图片_20220504162039.jpg",
      tableData: [
        {
          date: "2022-5-10",
          id: "椅子_1",
          address1: "(123,456,789)",
          address2: "(123, 123,123)",
        },
        {
          date: "2022-4-17",
          id: "广告牌_2",
          address1: "(12,13,14)",
          address2: "(17, 23, 90)",
        },
        {
          date: "2022-3-12",
          id: "椅子_1",
          address1: "(14, 231, 89)",
          address2: "(132,32,56)",
        },
        {
          date: "2022-1-1",
          id: "椅子_4",
          address1: "(14, 98, 45)",
          address2: "(92, 91, 78)",
        },
      ],
    };
  },
  methods: {
    upload() {
      console.log('上传视频');
      this.dialogVisible = true;
    }
  }
};
</script>

<style>
</style>
