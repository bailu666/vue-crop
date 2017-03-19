<template>
  <div id="app">
    <h1> vue 头像裁剪与预览</h1>
    <div class="item">
      <Upload url="https://httpbin.org/post" img-format="png"
        @crop-success="cropSuccess"
        @crop-upload-success="cropUploadSuccess"
        @crop-upload-fail="cropUploadFail"
        field="avatar1"
        ki="0"
        v-model="show1"
        :headers="headers"
        :params="otherParams"></Upload>
    </div>
    <div class="img_pro">
      <img class="avatar" v-if="avatarUrl1" :src="avatarUrl1" v-show="true" >
    </div>
  </div>
</template>

<script>
  import Upload from './components/Upload'

  export default {

  data:function() {
    return {
      show1: false,
      avatarUrl1: null,
      otherParams: {
        token: '123456798',
        name: 'img'
      },
      headers: {
        smail: '*_~'
      }

    } 
  },  
   components : {
        'Upload':Upload,
    },
    methods: {
    toggleShow1() {
      let {show1} = this;
      this.show1 = !show1;
    },
    cropSuccess(data, field, key) {
      if (field == 'avatar1') {
        this.avatarUrl1 = data;
      } 
    },
    cropUploadSuccess(data, field, key) {
      console.log('-------- 上传成功 --------');
      console.log(data);
      console.log('field: ' + field);
      console.log('key: ' + key);
    },
    cropUploadFail(status, field, key) {
      console.log('-------- 上传失败 --------');
      console.log(status);
      console.log('field: ' + field);
      console.log('key: ' + key);
    }
  }
  }
</script>

<style>

* {
      margin: 0;
      padding: 0;
    }

    body {
      font-family: '微软雅黑';
    }
    #app {
      width: 500px;
      margin: 50px auto;
      position: relative;
      text-align: center;
    }
    #app h1{
      line-height: 180px;
    }
    .wrap {
      margin-bottom: 5px;
    }
    .img_pro{
      margin-top: 20px;
    }
    .img_pro img{
      border-radius:100%;
      border: 1px solid red;
    }

</style>
