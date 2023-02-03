<template>
  <div class="score">
    <div class="title">
      <p class="name">计算机网络</p>
      <p class="description">(总分：100分,限时：100分钟)</p>
      <p class="description">学生：大咸鱼</p>
    </div>
    <div class="total">
      <div class="look">
        本次考试成绩: <span>{{score}}</span>
        <el-button type="primary" style="float: right; " round size="small" @click="back">back</el-button>
      </div>
      <div>
        <div class="showList">
          <el-card style="width:740px ;margin-top: 10px;">
            <div class="tit">选择</div>
            <el-card style="width:700px ;">
              <span class="block" v-for="(item, index) in topic[1]" :key="index">
                <span class="num">{{index}}:</span>
                <span v-if="item['show']" class="flag" style="color: rgb(88, 237, 88);">√</span>
                <span v-else class="flag" style="color:red ;">×</span>
              </span>
            </el-card>
            <div class="tit">详析：</div>
            <el-card style="width:700px ;margin-top: 10px;">
              <el-table :data="topic[1]" height="250" border style="width: 100%">
                <el-table-column
                type="index"
                label="题号"
                width="60"
                >
              </el-table-column>
                <el-table-column prop="question" label="题目" width="180">
                </el-table-column>
                <el-table-column prop="rightAnswer" label="答案" width="80">
                </el-table-column>
                <el-table-column prop="level" label="难度" width="80">
                </el-table-column>
                <el-table-column prop="analysis" label="解析" :empty-text="emptyText">
                </el-table-column>
              </el-table>
            </el-card>
          </el-card>
        </div>
        <div class="showList">
          <el-card style="width:740px ;margin-top: 10px;">
          <div class="tit">填空</div>
          <el-card style="width:700px ;">
            <span class="block" v-for="(item, index) in topic[2]" :key="index">
              <span class="num">{{index}}:</span>
              <span v-if="item['show']" class="flag" style="color: green;">√</span>
              <span v-else class="flag" style="color:red ;">×</span>
            </span>
          </el-card>
          <div class="tit">详析：</div>
          <el-card style="width:700px ;margin-top: 10px;">
            <el-table :data="topic[2]" height="250" border style="width: 100%">
              <el-table-column
              type="index"
              label="题号"
              width="60"
              >
            </el-table-column>
              <el-table-column prop="question" label="题目" width="180">
              </el-table-column>
              <el-table-column prop="answer" label="答案" width="80">
              </el-table-column>
              <el-table-column prop="level" label="难度" width="80">
              </el-table-column>
              <el-table-column prop="analysis" label="解析" :empty-text="emptyText">
              </el-table-column>
            </el-table>
          </el-card>
        </el-card>
        </div>
        <div class="showList">
          <el-card style="width:740px ;margin-top: 10px;">
          <div class="tit">判断</div>
          <el-card style="width:700px ;">
            <span class="block" v-for="(item, index) in topic[3]" :key="index">
              <span class="num">{{index}}:</span>
              <span v-if="item['show']" class="flag" style="color: green;">√</span>
              <span v-else class="flag" style="color:red ;">×</span>
            </span>
          </el-card>
          <div class="tit">详析：</div>
          <el-card style="width:700px ;margin-top: 10px;">
            <el-table :data="topic[3]" height="250" border style="width: 100%">
              <el-table-column
              type="index"
              label="题号"
              width="60"
              >
            </el-table-column>
              <el-table-column prop="question" label="题目" width="180">
              </el-table-column>
              <el-table-column prop="answer" label="答案" width="80">
              </el-table-column>
              <el-table-column prop="level" label="难度" width="80">
              </el-table-column>
              <el-table-column prop="analysis" label="解析" :empty-text="emptyText">
              </el-table-column>
            </el-table>
          </el-card>
        </el-card>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    data () {
      return {
        isTransition: false, //是否渲染完成
        score: 0, //总分
        topic: {},
        showList: {},
        emptyText:'暂无解析'
      }
    },
    created () {

      this.init()
    },
    methods: {

      init () {
        this.score = localStorage.getItem('finalScore')
        this.topic = JSON.parse(localStorage.getItem('topic'))
        for (const key in this.topic) {
          for(let i=0;i<this.topic[key].length;i++){
            if(!this.topic[key][i]['analysis']){

              this.topic[key][i]['analysis'] = '暂无解析'
            }
          }
          
        }
        console.log(this.topic)
      },
      back () {
        this.$router.push('/student')
      }
    }
  }
</script>

<style lang="scss" scoped>
  .flag {

    border-left: none;
    margin: 0;

  }

  .num {
    background-color: #bccdda;
    margin: 0;
    padding: 0 2px 0 2px;
    border-radius: 4%;
  }

  .block {
    display: inline-block;
    margin: 10px 10px;

    border: 1px dashed gray;
    border-radius: 4px;
    width: 50px;
  }

  .tit {
    width: 60px;
    margin: 10px;
    text-align: center;
    border-radius: 5px;
    color: #fff;
    background-color: #409eff;
    border-color: #409eff;

  }

  .btn {
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .show {
    display: flex;
    justify-content: center;
    align-items: center;

    img {
      width: 160px;
      height: 160px;
    }

    .img1Transform {
      opacity: 1 !important;
      transform: translateX(30px) !important;
      transition: all 0.6s ease !important;
    }

    .img2Transform {
      opacity: 1 !important;
      transform: translateX(-30px) !important;
      transition: all 0.6s ease !important;
    }

    .img1 {
      margin-top: 70px;
      opacity: 0;
      transform: translateX(0px);
      transition: all 0.6s ease;
    }

    .img2 {
      margin-top: 30px;
      opacity: 0;
      transform: translateX(0px);
      transition: all 0.6s ease;
    }
  }

  .time {
    padding: 0px 70px;

    li {
      display: flex;
      justify-content: space-around;
      padding: 10px;
      margin: 20px 0px;
    }

    li:nth-child(1) {
      background-color: #fcf8e3;
    }

    li:nth-child(2) {
      background-color: #e9f5e9;
    }
  }

  .border {
    border: 6px solid #36aafd !important;
    transition: all 2s ease;
    width: 160px !important;
    height: 160px !important;
    transform: rotate(360deg) !important;
    opacity: 1 !important;
  }

  .score {
    max-width: 800px;
    margin: 0 auto;

    .title {
      margin: 60px 0px 30px 0px;
      display: flex;
      justify-content: center;
      align-items: center;
      flex-direction: column;

      .name {
        font-size: 26px;
        color: inherit;
        font-weight: 500;
      }

      .description {
        font-size: 14px;
        color: #888;
      }
    }

    .total {
      border: 1px solid #dbdbdb;
      background-color: #fff;
      padding: 40px;

      .look {
        border-bottom: 1px solid #dbdbdb;
        padding: 0px 0px 14px 14px;
        color: #36aafd;
      }

      .number {
        opacity: 0;
        border: 6px solid #fff;
        transform: rotate(0deg);
        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: column;
        margin: 0 auto;
        width: 160px;
        height: 160px;
        border-radius: 50%;
        margin-top: 80px;
        margin-bottom: 20px;
        transition: all 1s ease;

        span:nth-child(1) {
          font-size: 36px;
          font-weight: 600;
        }

        span:nth-child(2) {
          font-size: 14px;
        }
      }
    }
  }
</style>