<template lang="html">
  <div class="message">
    <div class="wall-bg">
        <div class="bg-cover issue hover" @click="isspeaking = ! isspeaking"></div>
    
            <div class="speakCard" v-for="item in allMessages">
              <el-card :body-style="{ padding: '0px' }">  
                <div style="padding: 14px;">
                  用户：<span>{{item.user}}</span>
                  <div class="bottom clearfix">
                    <p>{{item.message}}</p>
                    <time class="time">{{ item.time }}</time>
                  </div>
                </div>
              </el-card>
            </div>
        
            <section v-show = "isspeaking" class="comment">
              <div v-if="userCookie" class="comment-isLogined">
                <textarea v-model="newComment" placeholder="段子手，来段评论吧...."></textarea>
                <button class="toComment" @click="gotoComment()" type="button">评论</button>
              </div>
              <div v-else class="comment-noLogined">
                段子手，你还没有登录，请登录后再进行评论
              </div>
              <div class="comments">
                <h2>当前共有 <span class="number">{{commentLength}}</span> 条留言</h2>
                <router-link :to="{path: '/'}" class="othersay">
                  去登陆
                </router-link>
              </div>
            </section>

    </div>
  </div>
</template>

<script>
import navHeader  from '../../components/navHeader'
import navFooter  from '../../components/navFooter'
export default {
  data(){
    return{
      detailData: '',
      newComment: '',
      commentLength: '',
      comments: '',
      showLike: false,
      userCookie: '',
      currentDate: new Date(),
      isspeaking: false,
      allMessages: ''
    }
  },
  created(){
    // 检查是否登陆
    this.$http.get('/users/checkLogin').then((respond) => {
      if(respond.data.code == 200){
        this.userCookie = respond.data.message;
      }
    })
    this.$http.get('/index/index_detail_message').then((response) => {
      console.log(132)
      console.log(response)
        this.allMessages = response.data.data;
    })
  },
  components:{
    navHeader,
    navFooter
  },
  methods: {
    
    gotoComment(){
      if(this.newComment == ""){
        this.$message({
          message: '评论不能为空',
          type: 'error'
        });
        return;
      }
      console.log(this.newComment)
      this.$http.post('/index/index_speak',{
        messages: this.newComment,
        user: this.userCookie.username
      }).then((response) => {
        console.log(response.data);
        this.$message({
          message: '评论成功',
          type: 'success'
        });
        this.$http.get('/index/index_detail_message').then((response) => {
        this.allMessages = response.data.data;
    })
      })
    }
  },

    
}
</script>

<style lang="less" scoped>
  .message{
    height: 100%;
    .wall-bg {
      width: 100%;
      height: 100%;
      position: relative;
      background-image: url(../../assets/wall.png);
      .issue {
          width: 250px;
          height: 80px;
          background-image: url(../../assets/issue.png);
          position: absolute;
          left: 50%;
          top: 10px;
          z-index: 98;
          -webkit-transform: translateX(-50%);
          -ms-transform: translateX(-50%);
          transform: translateX(-50%);
          -webkit-transition: opacity .5s;
          transition: opacity .5s;
      }
      .bg-cover{
          background-repeat: no-repeat;
          background-position: 50%;
      }
      .hover {
          cursor: pointer;
      }
      .bg-cover {
        background-size: cover;
      }

       .time {
        font-size: 13px;
        color: #999;
      }
      
      .bottom {
        margin-top: 13px;
        line-height: 25px;
      }

      .button {
        padding: 0;
        float: right;
      }

      .image {
        width: 100%;
        display: block;
      }

      .clearfix:before,
      .clearfix:after {
          display: table;
          content: "";
      }
      
      .clearfix:after {
          clear: both
      }


    }
    .speakCard {
      width: 235px;
      height: 100px;
      
      .el-card {
        height: 100%;
        width: 100%;
        background-color: #7ce772;
      }
    }



.comment{
      position: absolute;
      top: 20%;
      left: 37.5%;
      height: 300px;
      width: 350px;
      padding: 20px;
      margin-bottom: 40px;
      background-color: #fff;
      h2{
        height: 50px;
        line-height: 50px;
        border-bottom: 1px solid #ccc;
        .number{
          color: #4fc08d;
        }
      }
      .comment-noLogined{
        height: 80px;
        line-height: 80px;
        text-align: center;
        color: #4fc08d;
        font-weight: bold;
      }
      .comment-isLogined{
        height: 220px;
        border-bottom: 1px solid #ccc;
        textarea{
          height: 120px;
          width: 330px;
          margin: 10px 0;
          padding: 10px;
          border: 1px solid #ccc;
          border-radius: 4px;
          outline: none;
          &:focus{
            border-color: #66afe9;
            box-shadow:  0 0 8px rgba(102, 175, 233, .6);
          }
        }
        button{
          margin-left: 120px;
        }
      }
      .comment-item{
        display: flex;
        border-bottom: 1px solid #f1f1f1;
        .img{
          flex: 0 0 40px;
          width: 40px;
          height: 40px;
          margin: 10px;
          border-radius: 50%;
          border-radius: 1px solid #4fc08d;
        }
        .comment-text{
          flex: 1;
          margin-top: 10px;
          .comment-author{
            margin-right: 10px;
            font-size: 14px;
            color: #4fc08d;
          }
          .comment-time{
            font-size: 14px;
            color: #999;
          }
          .comment-content{
            margin: 10px 0;
          }
        }
      }
    }

  }
</style>
