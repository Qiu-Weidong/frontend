<template>
  <div>
    <el-card shadow="hover" class="mgb20" style="height: 100%">
      <el-row>
        <!-- <el-col> -->
        <div>
          <el-avatar
            :size="100"
            src="https://pic3.zhimg.com/v2-085ecd1a09850885408915051f52e458_xl.jpg?source=32738c0c"
          ></el-avatar>

          <!-- <div class="ProfileHeader-contentHead">
            <h1 class="ProfileHeader-title">
              <span class="ProfileHeader-name">张三</span
              ><span class="ztext ProfileHeader-headline"></span>
            </h1>
          </div> -->
        </div>
      </el-row>

      <el-row :gutter="20" class="mgb20"
        ><el-col :span="6" :offset="6">
          <el-checkbox :v-model="checked">模型训练权限</el-checkbox></el-col
        ></el-row
      >
      <el-row :gutter="20" class="mgb20"
        ><el-col :span="6" :offset="6">
          <el-checkbox :v-model="checked">管理员权限</el-checkbox></el-col
        ></el-row
      >
      <el-row :gutter="20" class="mgb20"
        ><el-col :span="6" :offset="6">
          <el-checkbox :v-model="checked">查看视频权限</el-checkbox></el-col
        ></el-row
      >
      <el-row :gutter="20" class="mgb20"
        ><el-col :span="6" :offset="6">
          <el-checkbox :v-model="checked">浏览实时数据权限</el-checkbox></el-col
        ></el-row
      >
      <el-row :gutter="20" class="mgb20"
        ><el-col :span="6" :offset="6">
          <el-checkbox :v-model="checked">删除历史数据权限</el-checkbox></el-col
        ></el-row
      >
      <el-row>
        <el-button>取消</el-button>
        <el-button type="primary">修改</el-button>
        <!-- <el-button type="success">成功按钮</el-button>
        <el-button type="info">信息按钮</el-button>
        <el-button type="warning">警告按钮</el-button>
        <el-button type="danger">危险按钮</el-button> -->
      </el-row>
    </el-card>
  </div>
</template>

<script>
export default {
  name: "editpermission",
  setup() {
    return {
      checked: true,
    };
  },
};
</script>

<style>
.ProfileHeader-contentHead {
  position: relative;
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-align: center;
  -ms-flex-align: center;
  align-items: center;
  -webkit-box-pack: justify;
  -ms-flex-pack: justify;
  justify-content: space-between;
  margin-bottom: 16px;
}
.ProfileHeader-title {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-flex: 1;
  -ms-flex: 1 1;
  flex: 1 1;
  text-overflow: ellipsis;
  white-space: nowrap;
}
.ProfileHeader-name {
  font-size: 26px;
  font-weight: 600;
  font-synthesis: style;
}
</style>
