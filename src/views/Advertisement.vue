<template>
  <div style="padding-left: 20px;padding-top: 20px">
    <div style="font-size: 22px; font-weight: 600; display: inline-block;">
      选择模型：
    </div>
    <div style="font-size: 25px; font-weight: 600; display: inline-block;">
        <el-select v-model="modelselect" placeholder="请选择要查看的模型">
          <el-option label="BorderDet" value="BorderDet" />
          <el-option label="YOLOX" value="YOLOX" />
        </el-select>
    </div>
    <!-- BorderDet页面 -->
    <div v-show="modelselect === 'BorderDet'">
      <div style="margin-top: 25px;">
        <el-carousel :interval="4000" trigger="click" height="500px" arrow="hover">
            <el-carousel-item v-for="item in adverimg" :key="item">
                <img :src="item.name" @click="viewdetails(item)" alt="" title="点击了解更多" style="width: 100%; height: 100%; cursor: pointer;">
            </el-carousel-item>
        </el-carousel>
      </div>
      <el-row>
        <el-col :span="6">
          <div style="width: 200px; margin-top: 15px; font-size: 22px; font-weight: 600">
            模型精度
          </div>
        </el-col>
      </el-row>
      <el-row style="margin-top: 20px;">
        <el-table :data="tableData1" stripe border style="width: 50%; font-size: 18px;">
          <el-table-column prop="id" label="类别" width="335">
          </el-table-column>
          <el-table-column prop="date" label="精度（AP）" width="335">
          </el-table-column>
        </el-table>
        <el-table :data="tableData2" stripe border style="width: 50%; font-size: 18px;">
          <el-table-column prop="id" label="类别" width="335">
          </el-table-column>
          <el-table-column prop="date" label="精度（AP）" width="335">
          </el-table-column>
        </el-table>
      </el-row>
      <el-row>
        <el-col :span="6">
          <div style="width: 200px; margin-top: 15px; font-size: 22px; font-weight: 600">
            训练损失曲线
          </div>
        </el-col>
      </el-row>
      <el-row style="margin-top: 20px">
        <img src="https://cdn.jsdelivr.net/gh/Qiu-Weidong/pictures/images/毕设/5.jpg" style="width: 40%">
      </el-row>
      <el-dialog
        v-model="dialogVisible1"
        title="详细信息"
        width="70%"
      >
        <div>
          <img :src="current_item.intro_img" alt="" style="width: 100%; height: 100%;">
          <div class="detail_title">
            {{current_item.title}}
          </div>
          <div v-html="current_item.content" class="detail_content"></div>
        </div>
        <template #footer>
          <span>
            <el-button @click="dialogVisible1 = false">关闭</el-button>
          </span>
        </template>
      </el-dialog>
    </div>
    <!-- YOLOX页面 -->
    <div v-show="modelselect === 'YOLOX'">
      <div style="margin-top: 25px;">
          <el-carousel :interval="4000" trigger="click" height="500px" arrow="hover">
              <el-carousel-item v-for="item in adverimg_yolox" :key="item">
                  <img :src="item.name" @click="viewdetails(item)" alt="" title="点击了解更多" style="width: 100%; height: 100%; cursor: pointer;">
              </el-carousel-item>
          </el-carousel>
      </div>
      <el-row>
        <el-col :span="6">
          <div style="width: 200px; margin-top: 15px; font-size: 22px; font-weight: 600">
            模型精度
          </div>
        </el-col>
      </el-row>
      <el-row style="margin-top: 20px;">
        <el-table :data="tableData1_yolox" stripe border style="width: 50%; font-size: 18px;">
          <el-table-column prop="id" label="类别" width="335">
          </el-table-column>
          <el-table-column prop="date" label="精度（AP）" width="335">
          </el-table-column>
        </el-table>
        <el-table :data="tableData2_yolox" stripe border style="width: 50%; font-size: 18px;">
          <el-table-column prop="id" label="类别" width="335">
          </el-table-column>
          <el-table-column prop="date" label="精度（AP）" width="335">
          </el-table-column>
        </el-table>
      </el-row>
      <el-row>
        <el-col :span="6">
          <div style="width: 200px; margin-top: 15px; font-size: 22px; font-weight: 600">
            训练损失曲线
          </div>
        </el-col>
      </el-row>
      <el-row style="margin-top: 20px">
        <div
          ref="myChart"
          id="myChart"
          :style="{ width: '600px', height: '400px' }"
        ></div>
      </el-row>
      <el-dialog
        v-model="dialogVisible1"
        title="详细信息"
        width="70%"
      >
        <div>
          <img :src="current_item.intro_img" alt="" style="width: 100%; height: 100%;">
          <div class="detail_title">
            {{current_item.title}}
          </div>
          <div v-html="current_item.content" class="detail_content"></div>
        </div>
        <template #footer>
          <span>
            <el-button @click="dialogVisible1 = false">关闭</el-button>
          </span>
        </template>
      </el-dialog>
    </div>    
  </div>
</template>

<script>
import {ref} from 'vue'
import upload from '../views/Upload.vue'
import { getCurrentInstance, onMounted } from 'vue';

export default {
  name: "Advertisement_Yolox",
  components: {upload},
  data() {
    return {
      modelselect: 'BorderDet',
      current_item: {},
    }
  },
  setup() {
    const dialogVisible1 = ref(false)
    const inputValue = ref('')
    const dynamicTags = ref([])
    const inputVisible = ref(false)
    const circleinput = ref('')
    // 通过 internalInstance.appContext.config.globalProperties 获取全局属性或方法
    let internalInstance = getCurrentInstance();
    let echarts = internalInstance.appContext.config.globalProperties.$echarts;
 
    onMounted(() => {
      const dom = document.getElementById('myChart');
      const myChart = echarts.init(dom); // 初始化echarts实例
      const option = {
        // title: {
        //   text: '训练损失曲线'
        // },
        legend: {
          data: ['椅子', '广告牌', '充电箱', '花盆']
        },
        xAxis: {
          type: 'category',
          data: [10, 20, 30, 40, 50, 60, 70, 80, 90, 91, 92, 93, 94, 95, 96, 97, 98, 99, 100,]
        },
        yAxis: {
          type: 'value'
        },
        series: [
          {
            name: '椅子',
            data: [0.8718, 0.9079, 0.9079, 0.9083, 0.9084, 0.9086, 0.9088, 0.9089, 0.9090, 0.9090, 0.9091, 0.9091, 0.9091, 0.9091, 0.9091, 0.9091, 0.9091, 0.9091, 0.9091, 0.9091, 0.9091, 0.9091, 0.9091, 0.9091],
            type: 'line',
            smooth: true
          },
          {
            name: '广告牌',
            data: [0.6901, 0.8861, 0.8987, 0.8965, 0.8934, 0.8967, 0.8957, 0.8955, 0.8969, 0.8970, 0.8971, 0.8982, 0.9020, 0.9014, 0.9035, 0.9030, 0.9028, 0.9013, 0.8988, 0.9016, 0.8989, 0.8994, 0.8984, 0.8992],
            type: 'line',
            smooth: true
          },
          {
            name: '充电箱',
            data: [0.7819, 0.9560, 0.9091, 0.9545, 0.9956, 0.9988, 1.0000, 0.9999, 1.0000, 1.0000, 1.0000, 1.0000, 1.0000, 1.0000, 1.0000, 1.0000, 1.0000, 1.0000, 1.0000, 1.0000, 1.0000, 1.0000, 1.0000, 1.0000],
            type: 'line',
            smooth: true
          },
          {
            name: '花盆',
            data: [0.2778, 0.5447, 0.5996, 0.6344, 0.6651, 0.6628, 0.7152, 0.7137, 0.7693, 0.7660, 0.7634, 0.8267, 0.8350, 0.8364, 0.8334, 0.8217, 0.8370, 0.8446, 0.8471, 0.8486, 0.8507, 0.8481, 0.8510, 0.8515],
            type: 'line',
            smooth: true
          },
        ]
      };
      // 设置实例参数
      myChart.setOption(option);
    });
    return {
      dialogVisible1,
      inputValue,
      inputVisible,
      dynamicTags,
      circleinput,
      options: [
        {
          value: "选项1",
          label: "摄像机1",
        },
        {
          value: "选项2",
          label: "摄像机2",
        },
        
      ],
      tableData1: [
        {
          id: "椅子",
          date: "90",
        },
        {
          id: "花盆",
          date: "91",
        },
        {
          id: "广告牌",
          date: "86",
        },
        {
          id: "充电箱",
          date: "92",
        },
      ],
      tableData2: [
        {
          id: "小物体",
          date: "88",
        },
        {
          id: "中物体",
          date: "92",
        },
        {
          id: "大物体",
          date: "96",
        },
        {
          id: "总体精度",
          date: "98",
        },
      ],
      tableData1_yolox: [
        {
          id: "椅子",
          date: "90",
        },
        {
          id: "花盆",
          date: "91",
        },
        {
          id: "广告牌",
          date: "86",
        },
        {
          id: "充电箱",
          date: "92",
        },
      ],
      tableData2_yolox: [
        {
          id: "小物体",
          date: "88",
        },
        {
          id: "中物体",
          date: "92",
        },
        {
          id: "大物体",
          date: "96",
        },
        {
          id: "总体精度",
          date: "98",
        },
      ],
      adverimg: [
        {intro_img:'../src/assets/img/Border-intro.png' ,name:'https://cdn.jsdelivr.net/gh/Qiu-Weidong/pictures/images/毕设/2.jpg',id : 1, title: '使用BorderDet利用边界信息进行分类与定位操作', content: '&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;目前大部分的point-based目标检测算法(SSD, RetinaNet, FCOS)使用特征图的single-point进行定位和分类，但single-point特征可能没有足够多的信息来表达完整的实例以及实例的边界信息。很多研究通过各种手段补充single-point的特征表达能力，这些方法虽然能够提取更多的特征，但可能带来不必要的计算以及会受背景的影响。最关键的，这些方法都没有直接利用边界特征，而边界对于定位是十分重要的。为此，论文提出新的特征提取操作BorderAlign，可直接利用边界特征优化原本的single-point特征。<p>&nbsp;</p><h3>主要贡献：</h3><p>&nbsp;</p><ul><li>分析dense object detector的特征表达，展示边界特征对补强single-point特征的重要性。</li><li>提出新的特征提取操作BorderAlign，通过边界特征来优化网络特征，并基于BorderAlign提出高性能目标检测算法BorderDet。</li><li>在COCO数据集上，将BAM模块集成到FCOS和FPN中分别提升2.8AP和3.6AP，而集成到ResNext-101-DCN准确率为50.3AP，达到SOTA。</li></ul>'},
        {intro_img:'../src/assets/img/Border-process.png' ,name:'https://cdn.jsdelivr.net/gh/Qiu-Weidong/pictures/images/毕设/1.jpg',id : 2, title: 'BorderDet算法流程', content: '&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;BorderDet提出一种简单且通用的操作，来显示提取边界极限点的特征，精准定位物体的框。于是我们开始介绍这个工作的组成，从局部到整体的顺序。（BorderAlign->BAM->BorderDet）<p>&nbsp;</p><h3>BorderAlign</h3><p>&nbsp;</p><p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;这是本工作最核心的一个操作，用来显式、自适应的提取物体边界的特征。如上图右上角。对于一个特征图，通道个数为5xC，这是一个border-sensitive的特征图，分别对应物体4个边界特征和原始anchor点位置的特征。对于一个anchor点预测的一个框，我们把这个框的4个border对应在特征图上的特征分别做pooling操作。且由于框的位置是小数，所以该操作使用双线性插值取出每个border上的特征。如图所示，我们每条边会先选出5个待采样点，再对这5个待采样点取最大的值，作为该条边的特征，即每条边最后只会选出一个采样点作为输出。那么每个anchor点都会采样5个点的特征作为输出，即输出的通道数也为5xC个。</p><p>&nbsp;</p><h3>BAM(Border Alignment Module)</h3><p>&nbsp;</p><p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;对于来自于FPN的特征，borderAlign需要5xC的border-sensitive的特征图，所以需要将通道先升维，提取完后再降维。为了“最干净”的验证Border feature的有效性，BAM中使用1x1conv来做升降维，几乎不增加模型的计算量。最后还原到256通道，来做最终的边界的分类和回归。</p><p>&nbsp;</p><h3>流程概述：</h3><p>&nbsp;</p><ul><li>通过FCOS作为Baseline获得预测框</li><li>BAM模块需要将FCOS的框位置的输出作为输入，显示的提取该框边界上的特征。</li><li>BAM进行边界敏感预测。</li><li>BAM得到的预测框与原始FCOS得到的预测框进行组合输出。</li></ul>'},
        {intro_img:'../src/assets/img/Border-rec.png' ,name:'../src/assets/img/Border-rec.png',id : 3, title:'特别的标注方式带来更方便快速的定位算法', content: '&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;本项目的标注工作对椅子边上的椅子支架进行标注，使椅子支架成为检测椅子的目标。这样做既使得标注框所包含的非目标信息减少，又更加方面确定目标物体的角点，从而目标定位算法可以使用角点去确定目标物体的真实世界坐标。既可以减少背景信息的干扰，又可以方便项目后续对于目标的定位操作。'},
        {intro_img:'https://cdn.jsdelivr.net/gh/Qiu-Weidong/pictures/images/毕设/4.jpg' ,name:'https://cdn.jsdelivr.net/gh/Qiu-Weidong/pictures/images/毕设/4.jpg',id : 4, title: "特征图可视化", content: "&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;为了对BorderDet算法能否能够通过提取边界特征来对目标的特征信息进行增强进行了验证，本文根据BorderDet源码开发了可视化特征图的接口，使得在预测过程中使用的特征图能够输出为图像，来判断是否提取了边界特征，可视化结果如图所示。<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;可以看到BorderDet确实可以显式提取到特征图向量，来对于预测时的单点特征信息进行增强，从而提高对于目标的检测精度。上图从左到右依次是BorderDet算法提取到的目标物体上边界、下边界、右边界、左边界的特征信息。</p>"},
      ],
      adverimg_yolox: [
        {intro_img:'../src/assets/img/yolox_intro.png' ,name:'../src/assets/img/yolox_intro.png',id : 1, title: '使用YOLOX提升对小目标的检测精度', content: '&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;本文研究的目标检测算法需要检测的目标包括花盆这类小目标，同时，距离摄像头较远的待检测物体在图像中也具有较小的形状，故要求研究的目标检测算法需要对小目标具有较高的检测精度。YOLOX是用来解决密集目标检测的高精度、高速率算法，拥有着对于小目标的较高检测精度，故在对于花盆的检测中，使用YOLOX进行目标检测模型训练。<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;YOLO系列是最先出现的单阶段目标检测方法，它大大提升了目标检测的速度，是第一个实现实时目标检测的方法。自YOLO系列诞生以来，已经有YOLOv1到YOLOv5多个版本，这些算法的性能及适用的应用环境各不相同。近年，人们又提出了YOLOX算法，YOLOX在YOLOv3的基础上加以改进，其性能超过了前面提到的YOLO系列所有的算法。</p>'},
        {intro_img:'../src/assets/img/yolox-pro.png' ,name:'../src/assets/img/yolox-pro.png',id : 2, title: 'YOLOX算法流程', content: '&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;BorderDet提出一种简单且通用的操作，来显示提取边界极限点的特征，精准定位物体的框。于是我们开始介绍这个工作的组成，从局部到整体的顺序。（BorderAlign->BAM->BorderDet）<p>&nbsp;</p><h3>输入端</h3><p>&nbsp;</p><p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在YOLOX的输入端采用了 Mosaic、Mixup两种数据增强方式，采用了这两种数据增强，直接相对于YOLO系列的精度提升了2.4个百分点</p><p>&nbsp;</p><h3>Backbon部分</h3><p>&nbsp;</p><p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在Backbone部分，YOLOX使用Darknet53网络结构。Darknet53网络使用步长为2的卷积层替代了原本的最大值池化层，使得它可以保留相对更多的信息，由此取得了更好的效果。相对于ResNet-101网络来说，运行速度有了显著的提升。</p><p>&nbsp;</p><h3>Neck部分</h3><p>&nbsp;</p><p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Neck对图像特征进行一系列混合。YOLOX的Neck部分使用的是FPN（特征金字塔）对图像特征进行混合。特征金字塔将处于高层的特征信息，通过上采样的方式进行，最终得到进行预测的特征图。</p><p>&nbsp;</p><h3>Prediction部分</h3></p></p><p>&nbsp;</p><p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;首先，YOLOX采用了Decoupled Head（解耦头）结构，该结构将目标检测的定位和分类任务分开，使用不同的特征图来进行任务，以此来解决由于定位和分类所关注内容不一致导致的问题。实验证明这一结构可以提高YOLO算法的准确度。其次YOLOX是基于anchor-free的目标检测器。YOLOX的anchor-free解决了通用性不好以及复杂度较高的问题，并能够取得更优的结果。</p>'},
      ],
    };
  },

  methods: {
    // jump() {
    //   this.$router.push('/ad_yolox')
    // },
    viewdetails(item) {
      this.dialogVisible1 = true;
      this.current_item = item;
    },
    handlecommand(command) {
      this.modelselect = command
      console.log(this.modelselect);
    },
    viewdialog() {
      this.dialogVisible1 = true
      console.log(this.dialogVisible1);
    },
    multi() {
      this.$router.push("/CCTVMulti");
    },
    showInput() {
      this.inputVisible = true
    },
    handleInputConfirm() {
      if (this.inputValue) {
        this.dynamicTags.push(this.inputValue)
      }
      this.inputVisible = false
      this.inputValue = ''
    },
    handleTagClose(index) {
      this.dynamicTags.splice(index, 1)
    },
  },
};
</script>

<style scoped>
  .example-showcase .el-dropdown-link {
    cursor: pointer;
    color: var(--el-color-primary);
    display: flex;
    align-items: center;
  }
  .demonstration {
    color: var(--el-text-color-secondary);
  }
  .el-carousel__item h3 {
    color: #475669;
    opacity: 0.75;
    line-height: 150px;
    margin: 0;
    text-align: center;
  }
  .propset {
    margin-top: 20px;
  }
  .submit-font {
    font-size: 20px;
    margin-bottom: 20px;
  }
  .title {
    height: 50px;
    width: 200px; 
    line-height: 50px;
    font-size: 30px;
    font-family: PingFang SC;
    letter-spacing: 2px;
    font-weight: 700;
    background-color: #f0f0f0;
  }
  .w-20 {
    width: 20%;
  }
  .detail_title {
    text-align: center;
    font-size: 30px;
    font-weight: 800;
    color: black;
    margin-top: 20px;
    margin-bottom: 20px;
  }
  .detail_content {
    font-size: 22px;
    margin-left: 100px;
    margin-right: 100px;
  }
</style>