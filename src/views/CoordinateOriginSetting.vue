<template>
  <div>
    <!-- 输入坐标 -->
    <el-raw>
      <el-form ref="point" :model="point" label-width="80px">
        <el-form-item> 手动输入坐标原点 </el-form-item>
        <el-form-item label="x坐标">
          <el-input v-model="point.x"></el-input>
        </el-form-item>
        <el-form-item label="y坐标">
          <el-input v-model="point.y"></el-input>
        </el-form-item>
        <el-form-item> 或者使用我们提供的坐标原点 </el-form-item>
        <el-form-item>
          <el-radio v-model="radio" label="1">墙角1</el-radio>
          <el-radio v-model="radio" label="2">墙角2</el-radio>
          <el-radio v-model="radio" label="3">柱子1</el-radio>
          <el-radio v-model="radio" label="4">柱子2</el-radio>
          <el-radio v-model="radio" label="5">柱子3</el-radio>
          <el-radio v-model="radio" label="6">柱子4</el-radio>
        </el-form-item>
        <el-form-item>
          <el-button type="primary" @click="onSubmit">确认设置</el-button>
          <el-button>取消</el-button>
        </el-form-item>
      </el-form>
    </el-raw>

    <el-raw>
      <el-image
        src="https://cdn.jsdelivr.net/gh/Qiu-Weidong/pictures/images/毕设/坐标原点设置.JPG"
      ></el-image>
    </el-raw>
    <el-raw>
      <el-table :data="tableData" style="width: 100%">
        <el-table-column prop="point" label="点" width="360"> </el-table-column>
        <el-table-column prop="coordinate" label="坐标/米"> </el-table-column>
      </el-table>
    </el-raw>
  </div>
</template>

<script>
export default {
  data() {
    return {
      point: { x: "", y: "" },
      tableData: [
        { point: "A", coordinate: "(12, 12)" },
        { point: "B", coordinate: "(24, 24)" },
        { point: "C", coordinate: "(36, 12)" },
        { point: "D", coordinate: "(12, 24)" },
        { point: "E", coordinate: "(12, 36)" },
        { point: "F", coordinate: "(12, 48)" },
        { point: "G", coordinate: "(36, 12)" },
        { point: "H", coordinate: "(36, 24)" },
        { point: "I", coordinate: "(36, 36)" },
      ],
    };
  },
};
</script>

<style>
</style>
