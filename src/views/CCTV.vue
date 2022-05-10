<template>
  <div>
    <el-row>
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
        <el-table-column prop="date" label="日期" width="180">
        </el-table-column>
        <el-table-column prop="id" label="物体id" width="180">
        </el-table-column>
        <el-table-column prop="address1" label="移动前坐标" width="180">
        </el-table-column>
        <el-table-column prop="address2" label="移动后坐标"> </el-table-column>
      </el-table>
    </el-row>
    <el-row>
      <!-- <el-col :offset="16"> -->
        <el-button>更多</el-button>
      <!-- </el-col> -->
    </el-row>
  </div>
</template>

<script>
export default {
  name: "CCTV",
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
    multi() {
      this.$router.push("/CCTVMulti");
    },
  },
};
</script>

<style>
</style>