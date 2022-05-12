<template>
    <div>
        <div class="container">
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
        </div>
    </div>
</template>

<script>
import { ref } from "vue";
import VueCropper from "vue-cropperjs";
import "cropperjs/dist/cropper.css";
import defaultSrc from "../assets/img/img.jpg";
export default {
    name: "upload",
    components: {
        VueCropper,
    },
    setup() {
        const imgSrc = ref("");
        const cropImg = ref(defaultSrc);
        const dialogVisible = ref(false);
        const cropper = ref(null);

        const setImage = (e) => {
            const file = e.target.files[0];
            if (!file.type.includes("image/")) {
                return;
            }
            const reader = new FileReader();
            reader.onload = (event) => {
                dialogVisible.value = true;
                imgSrc.value = event.target.result;
                cropper.value && cropper.value.replace(event.target.result);
            };
            reader.readAsDataURL(file);
        };

        const cropImage = () => {
            cropImg.value = cropper.value.getCroppedCanvas().toDataURL();
        };

        const cancelCrop = () => {
            dialogVisible.value = false;
            cropImg.value = defaultSrc;
        };

        return {
            cropper,
            imgSrc,
            cropImg,
            dialogVisible,
            setImage,
            cropImage,
            cancelCrop,
        };
    },
};
</script>

<style scoped>
.upload-demo {
    margin: 0 auto;
}
.content-title {
    font-weight: 400;
    line-height: 50px;
    margin: 10px 0;
    font-size: 22px;
    color: #1f2f3d;
}

.pre-img {
    width: 100px;
    height: 100px;
    background: #f8f8f8;
    border: 1px solid #eee;
    border-radius: 5px;
}
.crop-demo {
    display: flex;
    align-items: flex-end;
}
.crop-demo-btn {
    position: relative;
    width: 100px;
    height: 40px;
    line-height: 40px;
    padding: 0 20px;
    margin-left: 30px;
    background-color: #409eff;
    color: #fff;
    font-size: 14px;
    border-radius: 4px;
    box-sizing: border-box;
}
.crop-input {
    position: absolute;
    width: 100px;
    height: 40px;
    left: 0;
    top: 0;
    opacity: 0;
    cursor: pointer;
}
</style>