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
    </el-row>
    <el-row>
      <el-table :data="tableData" stripe style="width: 100%">
        <el-table-column prop="date" label="日期" width="“240”">
        </el-table-column>
        <el-table-column prop="id" label="物体id" width="“240”">
        </el-table-column>
        <el-table-column prop="address1" label="移动之前坐标" width="“240”">
        </el-table-column>
        <el-table-column prop="address2" label="移动之后坐标" width="“240”">
        </el-table-column>

        <el-table-column fixed="right" label="操作" width="120">
          <!-- <template slot-scope="scope"> -->
            <el-button type="text" size="small"> 详情 </el-button>
          <!-- </template> -->
        </el-table-column>
      </el-table>
    </el-row>
  </div>
</template>

<script>
export default {
  name: "VideoList",
  setup() {
    return {
      value: "",
      tableData: [
        {
          id: "椅子_1",
          date: "2022-5-11",
          address1: "(123,456,789)",
          address2: "(123, 789, 456)",
        },
        {
          id: "椅子_1",
          date: "2022-5-11",
          address1: "(123,456,789)",
          address2: "(123, 789, 456)",
        },
        {
          id: "椅子_1",
          date: "2022-5-11",
          address1: "(123,456,789)",
          address2: "(123, 789, 456)",
        },
        {
          id: "椅子_1",
          date: "2022-5-11",
          address1: "(123,456,789)",
          address2: "(123, 789, 456)",
        },
        {
          id: "椅子_1",
          date: "2022-5-11",
          address1: "(123,456,789)",
          address2: "(123, 789, 456)",
        },
        {
          id: "椅子_1",
          date: "2022-5-11",
          address1: "(123,456,789)",
          address2: "(123, 789, 456)",
        },
        {
          id: "椅子_1",
          date: "2022-5-11",
          address1: "(123,456,789)",
          address2: "(123, 789, 456)",
        },
        {
          id: "椅子_1",
          date: "2022-5-11",
          address1: "(123,456,789)",
          address2: "(123, 789, 456)",
        },
      ],
    };
  },
};
</script>

<style>
</style>