<template>
  <div>
    <el-dialog v-model="dialogVisible" width="70%">
      <video id="mse" autoplay="true" playsinline controls="controls" style="width:100%">
      <source
        src="../assets/img/video.mp4"
        type="video/mp4"
      />
      你的浏览器不支持Video标签
    </video>
    </el-dialog>
    <el-row>
      <el-button @click="multi">下载视频</el-button>
    </el-row>

    <el-row>
      <el-col :span="16">
        <video
        id="mse"
        autoplay="true"
        playsinline
        controls="controls"
        style="width: 100%"
      >
        <source src="../assets/img/video.mp4" type="video/mp4" />
        你的浏览器不支持Video标签
      </video>
      </el-col>
      <el-col :span="8">
      <el-card class="box-card">
          <!-- <div v-for="o in 4" :key="o" class="text item">
            {{ "列表内容 " + o }}
          </div> -->
          <h1>说明</h1>
          左侧是一条视频数据。下方的表格是这条视频中的相关报警数据。点击对应的条目可以查看目标移动的那十秒钟的视频。
        </el-card>
      </el-col>
    </el-row>

    <!-- <el-row v-if="multi" >
        <el-image style="width: 50%" :src="url" fit="contain"></el-image>
        <el-image style="width: 50%" :src="url" fit="contain"></el-image>
    </el-row> -->

    <el-row>
      <el-table :data="tableData" style="width: 100%">
        <el-table-column prop="date" label="日期" width="180">
        </el-table-column>
        <el-table-column prop="time" label="时间" width="180">
        </el-table-column>
        <el-table-column prop="id" label="物体id" width="180">
        </el-table-column>
        <el-table-column prop="address1" label="移动前坐标" width="180">
        </el-table-column>
        <el-table-column prop="address2" label="移动后坐标" width="180">
        </el-table-column>
        <el-table-column fixed="right" label="操作">
          <el-button type="text" size="small" @click="show">
            查看发生移动的那段视频
          </el-button>
        </el-table-column>
      </el-table>
    </el-row>
    <!-- <el-row>
      <el-button>更多</el-button>
    </el-row> -->
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  name: "VideoDetail",
  setup() {
    const dialogVisible = ref(false);
    return {
      dialogVisible,
      url: "https://cdn.jsdelivr.net/gh/Qiu-Weidong/pictures/images/毕设/微信图片_20220504162039.jpg",
      tableData: [
        {
          date: "2022-5-10",
          time: "16:35:17",
          id: "椅子_1",
          address1: "(123,456,0)",
          address2: "(123, 123,0)",
        },
        {
          date: "2022-5-10",
          time: "16:23:17",
          id: "广告牌_2",
          address1: "(12,13,0)",
          address2: "(17, 23, 0)",
        },
        {
          date: "2022-5-10",
          time: "16:35:23",
          id: "椅子_1",
          address1: "(14, 231, 89)",
          address2: "(132,32,56)",
        },
        {
          date: "2022-5-10",
          time: "16:32:17",
          id: "椅子_4",
          address1: "(14, 98, 45)",
          address2: "(92, 91, 78)",
        },
      ],
    };
  },
  methods: {
    show() {
      console.log("查看发生移动的那段视频");
      this.dialogVisible = true;
    },
  },
};
</script>

<style>
.box-card {
  /* width: 480px; */
  height: 90%;
  margin: 5% 5% 5% 5%;
}
</style>
