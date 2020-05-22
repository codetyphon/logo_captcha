<template>
  <div class="home">
    <br />
    <h1>品牌验证码</h1>
    <h2>{{ title }}</h2>
    <br />
    <div class="border">
      <div class="imgs">
        <Imgitem
          @child-event="evt"
          v-for="(img,index) in images"
          :key="index"
          :index="index"
          msg="hello"
          :img="img.src"
        />
      </div>
      <img v-show="is_success" class="good" src="../assets/good.jpg" />
    </div>
    <br />
    <br />
    <Button
      type="primary"
      v-show="!is_success"
      @click="ok"
      :disabled="isdisabled"
      shape="circle"
    >我选好了</Button>
    <Button type="primary" v-show="is_success" @click="restart" shape="circle">再来一次</Button>
  </div>
</template>

<script>
import axios from 'axios';
// @ is an alias to /src
import Imgitem from "@/components/Img.vue";

export default {
  name: "Home",
  components: {
    Imgitem
  },
  data() {
    return {
      title: "",
      jsons: [],
      images: [],
      checks: [],
      isdisabled: false,
      is_success: false
    };
  },
  methods: {
    evt(data, index) {
      // console.log(data, index);
      this.checks[index] = data;
    },
    ok() {
      this.isdisabled = true;
      let f = true;
      console.log(this.checks);
      this.checks.forEach((element, index) => {
        // console.log(element, index);
        if (element != this.images[index].flag) {
          f = false;
        }
      });
      if (f) {
        //ok
        this.$Message["success"]({
          background: true,
          duration: 2,
          content: "你选对啦"
        });
        this.is_success = true;
        console.log("success");
      } else {
        //err
        console.log("err");
        this.$Message["error"]({
          background: true,
          duration: 2,
          content: "你的选择不正确"
        });
        this.load(1000);
      }
    },
    load(time) {
      this.jsons.sort(function() {
        return Math.random() - 0.5;
      });
      setTimeout(() => {
        this.title = this.jsons[0].title;
        this.images = this.jsons[0].images;
        this.images.sort(function() {
          return Math.random() - 0.5;
        });
        this.checks = [
          false,
          false,
          false,
          false,
          false,
          false,
          false,
          false,
          false
        ];
        this.isdisabled = false;
      }, time);
    },
    restart() {
      this.is_success = false;
      this.load(1);
    }
  },
  created() {
    axios
      .get("images.json")
      .then(response => {
        console.log(response.data)
        this.jsons = response.data;
        this.load(0);
      });
  }
};
</script>

<style lang="scss">
.border {
  padding: 5px;
  width: 370px;
  height: 370px;
  margin: 0 auto;
  border-radius: 10px;
  box-shadow: 0 0 20px 5px #dcdcdc;
  position: relative;
}
.imgs {
  width: 360px;
  height: 360px;
  background: #000;
  border-radius: 5px;
  overflow: hidden;
  margin: 0 auto;
}
.red {
  color: red;
}
.good {
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
}
</style>