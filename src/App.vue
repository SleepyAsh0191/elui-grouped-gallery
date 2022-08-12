<template>
  <el-container>
    <el-header>Gallery</el-header>
    <el-main>
      <el-tabs class="nb-tab" v-model="activeName">
        <el-tab-pane
          v-for="item in contentData"
          :key="item.name"
          :label="item.name"
          :name="item.name"
        >
          <el-card class="box-card">
            <div v-for="obj in item.content" :key="obj.text" class="text item">
              <el-link
                @click="
                  if (obj.type == null)
                    pickImage(`./assets/pic/${obj.link}`, `${obj.text}`, `${obj.comment}`);
                  if (obj.type == 'audio')
                    pickImage(`./assets/audio/${obj.link}`, `${obj.text}`, `${obj.comment}`);
                  if (obj.type == 'video')
                    pickImage(`./assets/video/${obj.link}`, `${obj.text}`, `${obj.comment}`);
                  type = obj.type;
                "
                >{{ obj.text }}</el-link
              >
            </div>
          </el-card>
          <el-dialog v-model="dialogVisible" :title="dialogTitle">
            <span v-if="type == null">
              <el-image
                class="img"
                :src="image"
                v-if="image !== './assets/pic/#'"
                lazy
              />
            </span>
            <span v-else-if="type == 'audio'">
              <audio :src="image" controls="controls"></audio>
            </span>
            <span v-else>
              <video :src="image" controls="controls"></video>
            </span>
            <p v-if="comment != null" id="comment"></p>
          </el-dialog>
        </el-tab-pane>
      </el-tabs>
      <br />
    </el-main>
    <el-footer>
      <br />
      <el-tag>这里可以填写一些花里胡哨的信息</el-tag><br />
      <el-link href="https://beian.miit.gov.cn/"
        ><p>这里填写备案号</p></el-link
      ></el-footer
    >
  </el-container>
</template>

<script>
import { contentData } from "./data.js";
export default {
  data() {
    return {
      dialogTitle: "查看图片",
      contentData,
      activeName: "first",
      dialogVisible: false,
      image: "",
      type: null,
      comment: null
    };
  },
  methods: {
    pickImage(link, text, comment) {
      this.dialogTitle = `${text}`;
      this.dialogVisible = true;
      this.image = link;
      this.comment = comment;
      this.$el.querySelectorAll("#comment").forEach((item) => {
        if(comment == 'undefined'){
          item.innerText = "";
        } else {
          item.innerText = "评价：" + comment;
        }
      });
    },
  },
};
</script>

<style>
body {
  user-select: none;
  margin: 0 auto;
}

.el-container {
  margin-top: 10%;
}

.el-main {
  text-align: center;
}

.el-header,
.el-footer {
  background-color: rgb(239, 244, 250);
  text-align: center;
  line-height: 60px;
  margin-left: 10%;
  margin-right: 10%;
}

.el-footer {
  line-height: unset;
  height: 110px;
}

.el-tabs {
  margin-left: 10%;
  margin-right: 10%;
}

.text {
  font-size: 27px;
}

.img {
  max-height: 100%;
  max-width: 100%;
}

.kkj8 {
  max-height: 10%;
  max-width: 10%;
}
</style>
