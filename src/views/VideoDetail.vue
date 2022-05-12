<template>
  <div>
    <el-row>
    <el-button @click="multi">下载视频</el-button>
    </el-row>

    <el-row>
      <el-image style="width: 100%" :src="url" fit="contain"></el-image>
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
export default {
  name: "VideoDetail",
  setup() {
    return {
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
};
</script>

<style>
</style>
