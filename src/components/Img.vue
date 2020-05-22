<template>
  <div class="img" @click="click">
    <img class="pic" alt :src="img" />
    <!-- <div class="mask" v-show="!select"></div> -->
    <img
      :style="{top:y,left:x}"
      v-show="select"
      class="select"
      width="30"
      src="../assets/selected.png"
      alt
    />
  </div>
</template>

<script>
export default {
  name: "Img",
  props: {
    msg: String,
    img: String,
    index: Number,
    selectvalue:Boolean
  },
  data() {
    return {
      select: false,
      x: 0,
      y: 0
    };
  },
  methods: {
    click(event) {
      this.x = event.offsetX - 15 + "px";
      this.y = event.offsetY - 10 + "px";
      this.select = !this.select;
      this.$emit("child-event", this.select,this.index);
    }
  },watch:{
    img(val,oldval){
      if(val!=oldval){
        this.select=false
      }
    }
  }
};
</script>

<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.img {
  width: 120px;
  height: 120px;
  position: relative;
  float: left;
  cursor: pointer;
}
.pic {
  width: 120px;
  height: 120px;
  position: absolute;
  left: 0;
  top: 0;
  background: #fff;
}
.select {
  position: absolute;
  bottom: 10px;
  right: 10px;
}
.mask {
  position: absolute;
  top: 0;
  left: 0;
  width: 120px;
  height: 120px;
  background: #000;
  opacity: 0.3;
}
</style>
