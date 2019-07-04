<template lang="html">
  <div class="navHeader">
    <div class="container">
      <div class="left">
        <router-link to="/"><img src="../assets/time.gif" width="60" height="60" alt=""></router-link>
      </div>
      <div class="right">
        欢迎来到 我的个人 博客
      </div>

      <router-link :to="{path: '/speak'}" class="othersay">
        留言板
      </router-link>
      

      <div class="middle" @click='changeColor = !changeColor'>
        Aa
      </div>
      <div class="headerbox" v-if='changeColor'>
        <el-card class="box-card">
          <div slot="header" class="clearfix">
            <span style="margin-right: 15px;">夜间模式</span>
            <el-switch
              v-model="value"
              active-text="开"
              inactive-text="关"
              @change = "whatOff">
            </el-switch>
          </div>
          <div class="text item">
            <el-switch
              v-model="value1"
              active-text="宋体"
              inactive-text="黑体"
              @change = "whatFont">
            </el-switch>
            <div class="block" style="margin-top: 15px;">
              <span class="demonstration">亮度</span>
              <el-slider 
              v-model="value2"
              @change="whatLight">
              </el-slider>
            </div>
          </div>
        </el-card>
      </div>
      <!-- <div class="github">
        <a href="https://github.com/pengrongjie/vue-node-mongodb" target="_blank">
          <img src="../assets/github-logo.png" alt="">
        </a>
      </div> -->
    </div>
  </div>
</template>

<script>
export default {
  data(){
    return{
      changeColor: false,
      value: false,
      value1: false,
      value2: 37
    }
  },
  methods: {
    whatOff () {
      var list = document.getElementsByClassName("index_list")[0]
      if (this.value == false) {
        localStorage.setItem('whatOff', this.value)
        document.getElementById("app").style.backgroundColor = '#f5f5f5'
        
        document.getElementsByClassName("navHeader")[0].style.backgroundColor = '#fff'
        list.getElementsByClassName("left-item")[0].style.backgroundColor = '#f5f5f5'
        list.getElementsByClassName("left-item")[0].getElementsByTagName('a')[0].style.color = '#3f3f3f'
        list.getElementsByClassName("left-item")[1].style.backgroundColor = '#f5f5f5'
        list.getElementsByClassName("left-item")[1].getElementsByTagName('a')[0].style.color = '#3f3f3f'
        list.getElementsByClassName("left-item")[2].style.backgroundColor = '#f5f5f5'
        list.getElementsByClassName("left-item")[2].getElementsByTagName('a')[0].style.color = '#3f3f3f'
        list.getElementsByClassName("left-item")[3].style.backgroundColor = '#f5f5f5'
        list.getElementsByClassName("left-item")[3].getElementsByTagName('a')[0].style.color = '#3f3f3f'
        list.getElementsByClassName("left-item")[4].style.backgroundColor = '#f5f5f5'
        list.getElementsByClassName("left-item")[4].getElementsByTagName('a')[0].style.color = '#3f3f3f'
        document.getElementsByClassName("navHeader")[0].style.color = '#000'

        // document.getElementById("category-item").style.color = '#000'
        
      } else {
        this.value == true
        localStorage.setItem('whatOff', this.value)
        document.getElementById("app").style.backgroundColor = '#3f3f3f'

        document.getElementsByClassName("navHeader")[0].style.backgroundColor = '#3f3f3f'
        list.getElementsByClassName("left-item")[0].style.backgroundColor = '#3f3f3f'
        list.getElementsByClassName("left-item")[0].getElementsByTagName('a')[0].style.color = '#f5f5f5'
        list.getElementsByClassName("left-item")[1].style.backgroundColor = '#3f3f3f'
        list.getElementsByClassName("left-item")[1].getElementsByTagName('a')[0].style.color = '#f5f5f5'
        list.getElementsByClassName("left-item")[2].style.backgroundColor = '#3f3f3f'
        list.getElementsByClassName("left-item")[2].getElementsByTagName('a')[0].style.color = '#f5f5f5'
        list.getElementsByClassName("left-item")[3].style.backgroundColor = '#3f3f3f'
        list.getElementsByClassName("left-item")[3].getElementsByTagName('a')[0].style.color = '#f5f5f5'
        list.getElementsByClassName("left-item")[4].style.backgroundColor = '#3f3f3f'
        list.getElementsByClassName("left-item")[4].getElementsByTagName('a')[0].style.color = '#f5f5f5'
        document.getElementsByClassName("navHeader")[0].style.color = '#f5f5f5'   
        
        
      }
    },
    whatFont () {
      // if (this.value1 == false) {
      //   localStorage.setItem1('whatOff', this.value)
      //   document.getElementsByClassName("app").style.fontFamily = 'SimHei'
        
      // } else {
      //   this.value2 == true
      //   localStorage.setItem1('whatOff', this.value)
      //   document.getElementsByClassName("app").style.fontFamily = 'SimSun'
      // }
    },
    whatLight () {

    }
  },
  created() {
    localStorage.setItem('whatOff', this.value)
  },
}
</script>

<style lang="less" scoped>
.navHeader{
  height: 80px;
  background-color: #fff;
  box-shadow: 0 5px 5px rgba(0,0,0,0.07);
  color: #000;
  .left{
    float: left;
    img{
      margin: 10px;
    }
  }
  .right{
    float: left;
    line-height: 80px;
    margin: 0 20px;
    font-weight: bold;
  }
  .middle{
    float: right;
    line-height: 80px;
    margin: 0 20px;
    font-weight: bold;
    cursor: pointer;
  }
  .othersay{
    float: right;
    line-height: 80px;
    margin: 0 20px;
    font-weight: bold;
    cursor: pointer;
  }
  .headerbox {
    width: 300px;
    position: absolute;
    z-index: 999;
    top: 80px;
    right: 250px;
    .box-card {
      width: 100%;
      background-color: #3f3f3f;
      color: #fff;
    }
  }
  .github{
    float: right;
    img{
      width: 60px;
      height: 60px;
      display: block;
      margin: 10px;
    }
  }
}
</style>
