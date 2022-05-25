<template>
  <div>
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
    </el-row> -->

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
          左侧是一条视频数据。下方的表格展示了对视频中的目标进行识别和定位的过程，展示了坐标的变换过程。
        </el-card>
      </el-col>
    </el-row>

    <!-- <el-row v-if="multi" >
        <el-image style="width: 50%" :src="url" fit="contain"></el-image>
        <el-image style="width: 50%" :src="url" fit="contain"></el-image>
    </el-row> -->

    <el-row>
      <el-table :data="tableData" style="width: 100%">
        <el-table-column prop="id" label="物体id" width="180">
        </el-table-column>

        <el-table-column prop="coordinate1" label="像素坐标/像素" width="180">
        </el-table-column>
        <el-table-column prop="coordinate2" label="图像坐标/米" width="180">
        </el-table-column>

        <el-table-column prop="coordinate3" label="相机坐标/米" width="180">
        </el-table-column>
        <el-table-column prop="coordinate4" label="世界坐标/米">
        </el-table-column>
      </el-table>
    </el-row>
    <!-- <el-row>
      <el-button>更多</el-button>
    </el-row> -->
  </div>
</template>

<script>
export default {
  name: "Coordinate",
  setup() {
    return {
      url: "https://cdn.jsdelivr.net/gh/Qiu-Weidong/pictures/images/毕设/微信图片_20220504162039.jpg",
      options: [
        {
          value: "选项1",
          label: "摄像机1",
        },
        {
          value: "选项2",
          label: "摄像机2",
        },
        {
          value: "选项3",
          label: "摄像机3",
        },
        {
          value: "选项4",
          label: "摄像机4",
        },
        {
          value: "选项5",
          label: "摄像机5",
        },
      ],
      tableData: [
        {
          id: "椅子_1",
          coordinate1: "(375, 623)",
          coordinate2: "(153, 623)",
          coordinate3: "(123,456,789)",
          coordinate4: "(123, 123,123)",
        },
        {
          id: "广告牌_2",
          coordinate1: "(375, 623)",
          coordinate2: "(153, 623)",
          coordinate3: "(12,13,14)",
          coordinate4: "(17, 23, 90)",
        },
        {
          id: "椅子_1",
          coordinate1: "(375, 623)",
          coordinate2: "(153, 623)",
          coordinate3: "(14, 231, 89)",
          coordinate4: "(132,32,56)",
        },
        {
          id: "椅子_4",
          coordinate1: "(375, 623)",
          coordinate2: "(153, 623)",
          coordinate3: "(14, 98, 45)",
          coordinate4: "(92, 91, 78)",
        },
      ],
    };
  },

  methods: {
    multi() {
      this.$router.push("/CCTVMulti");
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