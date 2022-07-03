<template>
  <div>
    <el-row>
      <el-button @click="multi">全屏显示</el-button>
    </el-row>

    <!-- 分屏显示的视频 -->
    <el-row :gutter="20">
      <el-col :span="12">
        <el-raw>
          <el-select v-model="value" placeholder="请选择摄像头">
            <el-option
              v-for="item in options"
              :key="item.value"
              :label="item.label"
              :value="item.value"
            >
            </el-option>
          </el-select>
        </el-raw>
        <el-raw>
          <video
            id="mse"
            autoplay="true"
            playsinline
            controls="controls"
            style="width: 100%"
          >
            <source src="../assets/img/video2.mp4" type="video/mp4" />
            你的浏览器不支持Video标签
          </video>
        </el-raw>
      </el-col>
      <el-col :span="12">
        <el-raw>
          <el-select v-model="value" placeholder="请选择摄像头">
            <el-option
              v-for="item in options"
              :key="item.value"
              :label="item.label"
              :value="item.value"
            >
            </el-option>
          </el-select>
        </el-raw>
        <el-raw>
          <video
            id="mse"
            autoplay="true"
            playsinline
            controls="controls"
            style="width: 100%"
          >
            <source src="../assets/img/video3.mp4" type="video/mp4" />
            你的浏览器不支持Video标签
          </video>
        </el-raw>
      </el-col>
      <el-col :span="12">
        <el-raw>
          <el-select v-model="value" placeholder="请选择摄像头">
            <el-option
              v-for="item in options"
              :key="item.value"
              :label="item.label"
              :value="item.value"
            >
            </el-option>
          </el-select>
        </el-raw>
        <el-raw>
          <video
            id="mse"
            autoplay="true"
            playsinline
            controls="controls"
            style="width: 100%"
          >
            <source src="../assets/img/video4.mp4" type="video/mp4" />
            你的浏览器不支持Video标签
          </video>
        </el-raw>
      </el-col>
      <el-col :span="12">
        <el-raw>
          <el-select v-model="value" placeholder="请选择摄像头">
            <el-option
              v-for="item in options"
              :key="item.value"
              :label="item.label"
              :value="item.value"
            >
            </el-option>
          </el-select>
        </el-raw>
        <el-raw>
          <video
            id="mse"
            autoplay="true"
            playsinline
            controls="controls"
            style="width: 100%"
          >
            <source src="../assets/img/video1.mp4" type="video/mp4" />
            你的浏览器不支持Video标签
          </video>
        </el-raw>
      </el-col>
    </el-row>

    <el-row>
      <el-table :data="tableData" style="width: 100%">
        <el-table-column prop="date" label="日期"  width="180">
        </el-table-column>
        <el-table-column prop="time" label="时间"  width="180"></el-table-column>
        <el-table-column prop="camera" label="所属摄像头"  width="180">
        </el-table-column>

        <el-table-column prop="id" label="物体id"  width="180">
        </el-table-column>
        <el-table-column prop="address1" label="移动前坐标/米"  width="180">
        </el-table-column>
        <el-table-column prop="address2" label="移动后坐标/米">
        </el-table-column>
      </el-table>
    </el-row>
    <el-row>
      <el-button @click="more">更多</el-button>
    </el-row>
  </div>
</template>

<script>
export default {
  name: "CCTVMulti",
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
      ],
    };
  },

  methods: {
    multi() {
      this.$router.push("/CCTV");
    },
    more() {
      this.$router.push("/CCTVList");
    },
  },
};
</script>

<style>
</style>