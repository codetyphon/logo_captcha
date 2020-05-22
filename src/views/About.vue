<template>
  <div class="about">
    <h1>关于验证码</h1>
    <h2>用到的库：</h2>
    <p>vue</p>
    <p>vue-router</p>
    <p>ViewUI</p>
    <p>axios</p>
    <h2>用到的技术点：</h2>
    <p>
      <b>父组件向子组件传值</b>：
      <br />父：img="img.src"
      <br />子：props
      <br />
    </p>
    <p>
      <b>子组件向父组件传值</b>：
      <br />子：this.$emit("child-event", value);
      <br />父：@child-event="evt"
      <br />
    </p>
    <p>
      <b>组件内值变化的监控</b>：
      <br />watch
    </p>
  </div>
</template>
